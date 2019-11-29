---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Создание настраиваемых вспомогательных функций HTML (VB) | Документация Майкрософт
author: microsoft
description: Цель этого руководства — показать, как можно создавать пользовательские вспомогательные методы HTML, которые можно использовать в представлениях MVC. Используя преимущества вспомогательного метода HTML...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: aaeadde258a2855343a5bfb1e5ee76000e04f6bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593878"
---
# <a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="e79ba-104">Создание настраиваемых вспомогательных методов HTML (VB)</span><span class="sxs-lookup"><span data-stu-id="e79ba-104">Creating Custom HTML Helpers (VB)</span></span>

<span data-ttu-id="e79ba-105">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e79ba-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e79ba-106">Загрузить PDF-файл</span><span class="sxs-lookup"><span data-stu-id="e79ba-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="e79ba-107">Цель этого руководства — показать, как можно создавать пользовательские вспомогательные методы HTML, которые можно использовать в представлениях MVC.</span><span class="sxs-lookup"><span data-stu-id="e79ba-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="e79ba-108">Благодаря преимуществам вспомогательных функций HTML можно уменьшить объем утомительного ввода тегов HTML, которые необходимо выполнить для создания стандартной HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="e79ba-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="e79ba-109">Цель этого руководства — показать, как можно создавать пользовательские вспомогательные методы HTML, которые можно использовать в представлениях MVC.</span><span class="sxs-lookup"><span data-stu-id="e79ba-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="e79ba-110">Благодаря преимуществам вспомогательных функций HTML можно уменьшить объем утомительного ввода тегов HTML, которые необходимо выполнить для создания стандартной HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="e79ba-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="e79ba-111">В первой части этого руководства я опишу некоторые из существующих вспомогательных функций HTML, входящих в состав платформы MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e79ba-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="e79ba-112">Далее я опишу два метода создания настраиваемых вспомогательных методов HTML: я объясню, как создавать настраиваемые вспомогательные методы HTML, создав общий метод и создав метод расширения.</span><span class="sxs-lookup"><span data-stu-id="e79ba-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="e79ba-113">Основные сведения о вспомогательных возможностях HTML</span><span class="sxs-lookup"><span data-stu-id="e79ba-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="e79ba-114">Вспомогательный объект HTML — это просто метод, который возвращает строку.</span><span class="sxs-lookup"><span data-stu-id="e79ba-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="e79ba-115">Строка может представлять любой требуемый тип содержимого.</span><span class="sxs-lookup"><span data-stu-id="e79ba-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="e79ba-116">Например, с помощью вспомогательных функций HTML можно визуализировать стандартные HTML-теги, такие как HTML `<input>` и теги `<img>`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="e79ba-117">Кроме того, можно использовать вспомогательные средства HTML для визуализации более сложного содержимого, такого как полоса вкладок или таблица HTML данных базы данных.</span><span class="sxs-lookup"><span data-stu-id="e79ba-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="e79ba-118">Платформа ASP.NET MVC включает следующий набор стандартных вспомогательных функций HTML (это не полный список):</span><span class="sxs-lookup"><span data-stu-id="e79ba-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="e79ba-119">HTML. ActionLink ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-119">Html.ActionLink()</span></span>
- <span data-ttu-id="e79ba-120">HTML. Бегинформ ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-120">Html.BeginForm()</span></span>
- <span data-ttu-id="e79ba-121">HTML. CheckBox ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-121">Html.CheckBox()</span></span>
- <span data-ttu-id="e79ba-122">HTML. DropDownList ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-122">Html.DropDownList()</span></span>
- <span data-ttu-id="e79ba-123">HTML. Ендформ ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-123">Html.EndForm()</span></span>
- <span data-ttu-id="e79ba-124">HTML. Hidden ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-124">Html.Hidden()</span></span>
- <span data-ttu-id="e79ba-125">HTML. ListBox ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-125">Html.ListBox()</span></span>
- <span data-ttu-id="e79ba-126">HTML. Password ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-126">Html.Password()</span></span>
- <span data-ttu-id="e79ba-127">HTML. RadioButton ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-127">Html.RadioButton()</span></span>
- <span data-ttu-id="e79ba-128">HTML. TextArea ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-128">Html.TextArea()</span></span>
- <span data-ttu-id="e79ba-129">HTML. TextBox ()</span><span class="sxs-lookup"><span data-stu-id="e79ba-129">Html.TextBox()</span></span>

<span data-ttu-id="e79ba-130">Например, рассмотрим форму в листинге 1.</span><span class="sxs-lookup"><span data-stu-id="e79ba-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="e79ba-131">Эта форма отображается с помощью двух стандартных вспомогательных функций HTML (см. рис. 1).</span><span class="sxs-lookup"><span data-stu-id="e79ba-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="e79ba-132">В этой форме используются вспомогательные методы `Html.BeginForm()` и `Html.TextBox()`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>

<span data-ttu-id="e79ba-133">[Страница ![, отображаемая с помощью вспомогательных функций HTML](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e79ba-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="e79ba-134">**Рис. 01**. страница, отображаемая с помощью вспомогательных функций HTML ([щелкните, чтобы просмотреть изображение с полным размером](creating-custom-html-helpers-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e79ba-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>

<span data-ttu-id="e79ba-135">**Листинг 1 — `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="e79ba-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="e79ba-136">Вспомогательный метод `Html.BeginForm()` используется для создания открывающих и закрывающих тегов HTML `<form>`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="e79ba-137">Обратите внимание, что метод `Html.BeginForm()` вызывается в операторе using.</span><span class="sxs-lookup"><span data-stu-id="e79ba-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="e79ba-138">Оператор using гарантирует, что тег `<form>` закрывается в конце блока using.</span><span class="sxs-lookup"><span data-stu-id="e79ba-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="e79ba-139">При желании вместо создания блока using можно вызвать вспомогательный метод HTML. Ендформ (), чтобы закрыть тег `<form>`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="e79ba-140">Используйте любой из подходов к созданию открывающего и закрывающего тега `<form>`, который кажется наиболее интуитивно понятным для вас.</span><span class="sxs-lookup"><span data-stu-id="e79ba-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="e79ba-141">Вспомогательные методы `Html.TextBox()` используются в листинге 1 для отрисовки HTML-тегов `<input>`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="e79ba-142">Если в браузере выбрать пункт Просмотреть источник, появится источник HTML в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="e79ba-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="e79ba-143">Обратите внимание, что источник содержит стандартные теги HTML.</span><span class="sxs-lookup"><span data-stu-id="e79ba-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e79ba-144">Обратите внимание, что вспомогательный модуль `Html.TextBox()`-HTML подготавливается к просмотру с помощью тегов `<%= %>`, а не `<% %>` тегов.</span><span class="sxs-lookup"><span data-stu-id="e79ba-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="e79ba-145">Если не указать знак равенства, в браузере ничего не отображается.</span><span class="sxs-lookup"><span data-stu-id="e79ba-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="e79ba-146">Платформа ASP.NET MVC содержит небольшой набор вспомогательных функций.</span><span class="sxs-lookup"><span data-stu-id="e79ba-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="e79ba-147">Скорее всего, вам потребуется расширить платформу MVC с помощью настраиваемых вспомогательных функций HTML.</span><span class="sxs-lookup"><span data-stu-id="e79ba-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="e79ba-148">В оставшейся части этого руководства вы узнаете о двух методах создания пользовательских вспомогательных методов HTML.</span><span class="sxs-lookup"><span data-stu-id="e79ba-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="e79ba-149">**Листинг 2 — `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="e79ba-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="e79ba-150">Создание вспомогательных методов HTML с общими методами</span><span class="sxs-lookup"><span data-stu-id="e79ba-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="e79ba-151">Самый простой способ создания нового вспомогательного метода HTML — создать общий метод, возвращающий строку.</span><span class="sxs-lookup"><span data-stu-id="e79ba-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="e79ba-152">Представьте, например, что вы решили создать новый вспомогательный метод HTML, который визуализирует HTML-`<label>` тег.</span><span class="sxs-lookup"><span data-stu-id="e79ba-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="e79ba-153">Для отображения `<label>`можно использовать класс в листинге 2.</span><span class="sxs-lookup"><span data-stu-id="e79ba-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="e79ba-154">**Листинг 2 — `Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="e79ba-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="e79ba-155">В листинге 2 нет ничего особенного о классе.</span><span class="sxs-lookup"><span data-stu-id="e79ba-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="e79ba-156">Метод `Label()` просто возвращает строку.</span><span class="sxs-lookup"><span data-stu-id="e79ba-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="e79ba-157">Измененное представление индекса в листинге 3 использует `LabelHelper` для визуализации тегов HTML `<label>`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="e79ba-158">Обратите внимание, что представление содержит директиву `<%@ imports %>`, которая импортирует пространство имен Application1. Вспомогательныеs.</span><span class="sxs-lookup"><span data-stu-id="e79ba-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="e79ba-159">**Листинг 2 — `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="e79ba-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="e79ba-160">Создание вспомогательных функций HTML с помощью методов расширения</span><span class="sxs-lookup"><span data-stu-id="e79ba-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="e79ba-161">Если вы хотите создать вспомогательные методы HTML, которые работают точно так же, как стандартные вспомогательные методы HTML, входящие в платформу ASP.NET MVC, то вам нужно создать метод расширения.</span><span class="sxs-lookup"><span data-stu-id="e79ba-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="e79ba-162">Методы расширения позволяют добавлять новые методы в существующий класс.</span><span class="sxs-lookup"><span data-stu-id="e79ba-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="e79ba-163">При создании вспомогательного метода HTML в класс `HtmlHelper` добавляются новые методы, представленные свойством HTML представления.</span><span class="sxs-lookup"><span data-stu-id="e79ba-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="e79ba-164">Модуль Visual Basic в листинге 3 добавляет метод расширения с именем `Label()` в класс `HtmlHelper`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="e79ba-165">Есть несколько вещей, которые следует заметить при работе с этим модулем.</span><span class="sxs-lookup"><span data-stu-id="e79ba-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="e79ba-166">Во-первых, обратите внимание, что модуль снабжен атрибутом `<Extension()>`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="e79ba-167">Чтобы использовать этот атрибут, необходимо импортировать пространство имен `System.Runtime.CompilerServices`</span><span class="sxs-lookup"><span data-stu-id="e79ba-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="e79ba-168">Во вторых, обратите внимание, что первый параметр метода `Label()` представляет класс `HtmlHelper`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="e79ba-169">Первый параметр метода расширения указывает класс, который расширяет метод расширения.</span><span class="sxs-lookup"><span data-stu-id="e79ba-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="e79ba-170">**Листинг 3 — `Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="e79ba-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="e79ba-171">После создания метода расширения и успешного построения приложения метод расширения отображается в IntelliSense Visual Studio, как и все другие методы класса (см. рис. 2).</span><span class="sxs-lookup"><span data-stu-id="e79ba-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="e79ba-172">Единственное отличие заключается в том, что методы расширения отображаются с специальным символом рядом с ними (значок со стрелкой вниз).</span><span class="sxs-lookup"><span data-stu-id="e79ba-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="e79ba-173">[![с помощью метода расширения HTML. Label ()](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e79ba-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="e79ba-174">**Рис. 02**. использование метода расширения HTML. Label () ([щелкните, чтобы просмотреть изображение с полным размером](creating-custom-html-helpers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e79ba-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>

<span data-ttu-id="e79ba-175">Измененное представление индекса в листинге 4 использует метод расширения HTML. Label () для отображения всех &lt;меток&gt; тегов.</span><span class="sxs-lookup"><span data-stu-id="e79ba-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="e79ba-176">**Листинг 4 — `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="e79ba-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="e79ba-177">Сводка</span><span class="sxs-lookup"><span data-stu-id="e79ba-177">Summary</span></span>

<span data-ttu-id="e79ba-178">В этом руководстве вы узнали два метода создания пользовательских вспомогательных методов HTML.</span><span class="sxs-lookup"><span data-stu-id="e79ba-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="e79ba-179">Во-первых, вы узнали, как создать пользовательский вспомогательный модуль HTML `Label()`, создав общий метод, возвращающий строку.</span><span class="sxs-lookup"><span data-stu-id="e79ba-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="e79ba-180">Далее вы узнали, как создать пользовательский вспомогательный метод HTML `Label()`, создав метод расширения для класса `HtmlHelper`.</span><span class="sxs-lookup"><span data-stu-id="e79ba-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="e79ba-181">В этом учебнике мы посвящены созданию чрезвычайно простого вспомогательного метода HTML.</span><span class="sxs-lookup"><span data-stu-id="e79ba-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="e79ba-182">Следует понимать, что вспомогательный метод HTML может быть сложным.</span><span class="sxs-lookup"><span data-stu-id="e79ba-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="e79ba-183">Можно создавать вспомогательные средства HTML, которые отображают форматированное содержимое, например представления в виде дерева, меню или таблицы данных базы данных.</span><span class="sxs-lookup"><span data-stu-id="e79ba-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e79ba-184">[Назад](asp-net-mvc-views-overview-vb.md)
> [Вперед](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e79ba-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>
