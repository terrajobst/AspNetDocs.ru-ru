---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: Создание и использование вспомогательного метода на сайте веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой статье описывается создание вспомогательного приложения на веб-сайте веб-страницы ASP.NET (Razor). Вспомогательный объект — это многократно используемый компонент, который содержит код и разметку для производительности...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454308"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="9cbb0-104">Создание и использование вспомогательного метода на сайте веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="9cbb0-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="9cbb0-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9cbb0-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9cbb0-106">В этой статье описывается создание вспомогательного приложения на веб-сайте веб-страницы ASP.NET (Razor).</span><span class="sxs-lookup"><span data-stu-id="9cbb0-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="9cbb0-107">*Вспомогательное приложение* — это многократно используемый компонент, который содержит код и разметку для выполнения задачи, которая может быть утомительной или сложной.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="9cbb0-108">**Что вы узнаете:**</span><span class="sxs-lookup"><span data-stu-id="9cbb0-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="9cbb0-109">Как создать и использовать простой вспомогательный метод.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="9cbb0-110">Это функции ASP.NET, представленные в статье:</span><span class="sxs-lookup"><span data-stu-id="9cbb0-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="9cbb0-111">Синтаксис `@helper`.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9cbb0-112">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="9cbb0-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="9cbb0-113">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="9cbb0-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="9cbb0-114">Этот учебник также работает с веб-страницы ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="9cbb0-115">Обзор вспомогательных функций</span><span class="sxs-lookup"><span data-stu-id="9cbb0-115">Overview of Helpers</span></span>

<span data-ttu-id="9cbb0-116">Если необходимо выполнить те же задачи на разных страницах сайта, можно использовать вспомогательное приложение.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="9cbb0-117">Веб-страницы ASP.NET включает несколько вспомогательных функций, и вы можете скачать и установить гораздо больше.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="9cbb0-118">(Список встроенных вспомогательных функций в веб-страницы ASP.NET приведен в [кратком справочнике по API ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202907).) Если ни один из существующих вспомогательных функций не соответствует вашим потребностям, вы можете создать собственный модуль поддержки.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="9cbb0-119">Вспомогательный объект позволяет использовать общий блок кода на нескольких страницах.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="9cbb0-120">Предположим, что на странице часто требуется создать элемент примечания, который будет отделяться от обычных абзацев.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="9cbb0-121">Возможно, заметка создается как элемент `<div>`, оформленный как поле с границей.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="9cbb0-122">Вместо того, чтобы добавлять эту разметку на страницу каждый раз, когда нужно отобразить заметку, можно упаковать разметку как вспомогательную функцию.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="9cbb0-123">Затем можно вставить заметку с одной строкой кода там, где она нужна.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="9cbb0-124">Использование вспомогательного метода делает код на каждой из ваших страниц проще и проще в чтении.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="9cbb0-125">Кроме того, это упрощает обслуживание сайта, так как, если необходимо изменить вид заметок, можно изменить разметку в одном месте.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="9cbb0-126">Создание вспомогательного метода</span><span class="sxs-lookup"><span data-stu-id="9cbb0-126">Creating a Helper</span></span>

<span data-ttu-id="9cbb0-127">В этой процедуре показано, как создать вспомогательный объект, который создает заметку, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="9cbb0-128">Это простой пример, но пользовательский вспомогательный метод может содержать любую разметку и ASP.NET код, который вам нужен.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="9cbb0-129">В корневой папке веб-сайта создайте папку с именем *App\_Code*.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="9cbb0-130">Это зарезервированное имя папки в ASP.NET, где можно разместить код для таких компонентов, как вспомогательные методы.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="9cbb0-131">В папке *приложения\_код* создайте новый *CSHTML* -файл и назовите его *михелперс. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="9cbb0-132">Замените имеющееся содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="9cbb0-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="9cbb0-133">В коде используется синтаксис `@helper` для объявления нового вспомогательного метода с именем `MakeNote`.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="9cbb0-134">Этот конкретный вспомогательный метод позволяет передать параметр с именем `content`, который может содержать сочетание текста и разметки.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="9cbb0-135">Вспомогательная функция вставляет строку в текст заметки, используя переменную `@content`.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="9cbb0-136">Обратите внимание, что файл называется *михелперс. cshtml*, но вспомогательный объект называется `MakeNote`.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="9cbb0-137">В один файл можно добавить несколько пользовательских вспомогательных функций.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="9cbb0-138">Сохраните файл и закройте его.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="9cbb0-139">Использование вспомогательного метода на странице</span><span class="sxs-lookup"><span data-stu-id="9cbb0-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="9cbb0-140">В корневой папке создайте новый пустой файл с именем *TestHelper. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="9cbb0-141">Добавьте в него указанный ниже код.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="9cbb0-142">Чтобы вызвать созданный вспомогательный модуль, используйте `@`, за которым следует имя файла, в котором находится вспомогательная функция, точка, а затем имя вспомогательного метода.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="9cbb0-143">(Если в папке *\_приложения* имеется несколько папок, можно использовать синтаксис `@FolderName.FileName.HelperName` для вызова вспомогательного метода на любом уровне вложенной папки).</span><span class="sxs-lookup"><span data-stu-id="9cbb0-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="9cbb0-144">Текст, добавляемый в кавычки в круглых скобках, — это текст, который вспомогательный компонент будет отображать как часть заметки на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="9cbb0-145">Сохраните страницу и запустите ее в браузере.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="9cbb0-146">Вспомогательное приложение создает элемент примечания прямо там, где вы вызывали вспомогательное приложение: между двумя абзацами.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![Снимок экрана, показывающий страницу в браузере и то, как созданная вспомогательная функция помещает в рамку вокруг указанного текста.](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="9cbb0-148">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9cbb0-148">Additional Resources</span></span>

<span data-ttu-id="9cbb0-149">[Горизонтальное меню в качестве вспомогательного метода Razor](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span><span class="sxs-lookup"><span data-stu-id="9cbb0-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="9cbb0-150">В этой записи блога от Mike Поуп показано, как создать горизонтальное меню в качестве вспомогательного приложения с помощью разметки, CSS и кода.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="9cbb0-151">Использование [HTML5 в веб-страницы ASP.NET вспомогательных средах для WebMatrix и ASP.NET MvC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cbb0-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="9cbb0-152">В этой записи блога с помощью SAM Абрахам показан вспомогательный объект, который визуализирует элемент `Canvas` HTML5.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="9cbb0-153">[Разница между @Helpers и @Functions в WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span><span class="sxs-lookup"><span data-stu-id="9cbb0-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="9cbb0-154">В этой записи блога от Mike Бринд `@helper` описывается синтаксис и `@function` синтаксис и когда следует использовать каждый из них.</span><span class="sxs-lookup"><span data-stu-id="9cbb0-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
