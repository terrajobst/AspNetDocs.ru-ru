---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: Проверка вводимых пользователем данных на сайтах веб-страницы ASP.NET (Razor) | Документация Майкрософт
author: Rick-Anderson
description: В этой статье описано, как проверить сведения, получаемые от пользователей, &mdash; то есть убедиться, что пользователи вводят действительную информацию в HTML-формы как...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454302"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="6260d-103">Проверка вводимых пользователем данных на сайтах веб-страницы ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="6260d-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="6260d-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6260d-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6260d-105">В этой статье описано, как проверить сведения, получаемые от пользователей, &mdash; то есть убедиться, что пользователи вводят действительную информацию в HTML-формы на сайте веб-страницы ASP.NET (Razor).</span><span class="sxs-lookup"><span data-stu-id="6260d-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="6260d-106">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="6260d-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="6260d-107">Проверка того, соответствуют ли входные данные пользователя определенным условиям проверки.</span><span class="sxs-lookup"><span data-stu-id="6260d-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="6260d-108">Как определить, пройдены ли все проверочные тесты.</span><span class="sxs-lookup"><span data-stu-id="6260d-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="6260d-109">Как отобразить ошибки проверки (и способ их форматирования).</span><span class="sxs-lookup"><span data-stu-id="6260d-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="6260d-110">Проверка данных, которые не поступают непосредственно от пользователей.</span><span class="sxs-lookup"><span data-stu-id="6260d-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="6260d-111">Ниже приведены основные понятия программирования ASP.NET, представленные в статье:</span><span class="sxs-lookup"><span data-stu-id="6260d-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="6260d-112">Вспомогательный метод `Validation`.</span><span class="sxs-lookup"><span data-stu-id="6260d-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="6260d-113">Методы `Html.ValidationSummary` и `Html.ValidationMessage`.</span><span class="sxs-lookup"><span data-stu-id="6260d-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6260d-114">Версии программного обеспечения, используемые в этом руководстве</span><span class="sxs-lookup"><span data-stu-id="6260d-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6260d-115">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="6260d-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="6260d-116">Этот учебник также работает с веб-страницы ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="6260d-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="6260d-117">Эта статья состоит из следующих разделов:</span><span class="sxs-lookup"><span data-stu-id="6260d-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="6260d-118">Общие сведения о проверке вводимых пользователем данных</span><span class="sxs-lookup"><span data-stu-id="6260d-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="6260d-119">Проверка вводимых пользователем данных</span><span class="sxs-lookup"><span data-stu-id="6260d-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="6260d-120">Добавление проверки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="6260d-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="6260d-121">Ошибки проверки форматирования</span><span class="sxs-lookup"><span data-stu-id="6260d-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="6260d-122">Проверка данных, которые не приходят непосредственно от пользователей</span><span class="sxs-lookup"><span data-stu-id="6260d-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="6260d-123">Общие сведения о проверке вводимых пользователем данных</span><span class="sxs-lookup"><span data-stu-id="6260d-123">Overview of User Input Validation</span></span>

<span data-ttu-id="6260d-124">Если вы запрашиваете у пользователей ввод информации на странице (например, в форму), важно убедиться, что введенные значения допустимы.</span><span class="sxs-lookup"><span data-stu-id="6260d-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="6260d-125">Например, вы не хотите обрабатывать форму, в которой отсутствуют важные сведения.</span><span class="sxs-lookup"><span data-stu-id="6260d-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="6260d-126">Когда пользователь вводит значения в HTML-форму, вводимые им значения являются строками.</span><span class="sxs-lookup"><span data-stu-id="6260d-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="6260d-127">Во многих случаях нужными значениями являются другие типы данных, такие как целые числа или даты.</span><span class="sxs-lookup"><span data-stu-id="6260d-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="6260d-128">Поэтому необходимо также убедиться, что значения, вводимые пользователями, могут быть правильно преобразованы в соответствующие типы данных.</span><span class="sxs-lookup"><span data-stu-id="6260d-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="6260d-129">Кроме того, могут иметься определенные ограничения на значения.</span><span class="sxs-lookup"><span data-stu-id="6260d-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="6260d-130">Даже если пользователи правильно вводят целое число, например, может потребоваться убедиться в том, что значение попадает в определенный диапазон.</span><span class="sxs-lookup"><span data-stu-id="6260d-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![Ошибки проверки, использующие классы стилей CSS](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="6260d-132">**Важно!** Проверка вводимых пользователем данных также важна для обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="6260d-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="6260d-133">Если ограничить значения, которые пользователи могут вводить в формы, можно уменьшить вероятность того, что кто-то сможет ввести значение, которое может нарушить безопасность вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="6260d-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="6260d-134">Проверка введенного пользователем</span><span class="sxs-lookup"><span data-stu-id="6260d-134">Validating User Input</span></span>

<span data-ttu-id="6260d-135">В веб-страницы ASP.NET 2 можно использовать вспомогательный метод `Validator` для проверки вводимых пользователем данных.</span><span class="sxs-lookup"><span data-stu-id="6260d-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="6260d-136">Базовый подход состоит в следующем:</span><span class="sxs-lookup"><span data-stu-id="6260d-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="6260d-137">Определите, какие элементы ввода (поля) необходимо проверить.</span><span class="sxs-lookup"><span data-stu-id="6260d-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="6260d-138">Обычно значения проверяются в элементах `<input>` в форме.</span><span class="sxs-lookup"><span data-stu-id="6260d-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="6260d-139">Однако рекомендуется проверять все входные данные, даже входные данные, поступающие из ограниченного элемента, такого как список `<select>`.</span><span class="sxs-lookup"><span data-stu-id="6260d-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="6260d-140">Это помогает убедиться, что пользователи не обходят элементы управления на странице и не отправляют форму.</span><span class="sxs-lookup"><span data-stu-id="6260d-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="6260d-141">В коде страницы добавьте отдельные проверки для каждого элемента ввода с помощью методов вспомогательного метода `Validation`.</span><span class="sxs-lookup"><span data-stu-id="6260d-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="6260d-142">Чтобы проверить обязательные поля, используйте `Validation.RequireField(field, [error message])` (для отдельного поля) или `Validation.RequireFields(field1, field2, ...))` (для списка полей).</span><span class="sxs-lookup"><span data-stu-id="6260d-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="6260d-143">Для других типов проверки используйте `Validation.Add(field, ValidationType)`.</span><span class="sxs-lookup"><span data-stu-id="6260d-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="6260d-144">Для `ValidationType`можно использовать следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="6260d-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="6260d-145">При отправке страницы проверьте, пройдена ли проверка, проверив `Validation.IsValid`:</span><span class="sxs-lookup"><span data-stu-id="6260d-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="6260d-146">При наличии каких-либо ошибок проверки обработка страниц пропускается.</span><span class="sxs-lookup"><span data-stu-id="6260d-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="6260d-147">Например, если целью страницы является обновление базы данных, это не делается, пока не будут исправлены все ошибки проверки.</span><span class="sxs-lookup"><span data-stu-id="6260d-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="6260d-148">При наличии ошибок проверки выведите сообщения об ошибках в разметке страницы с помощью `Html.ValidationSummary` или `Html.ValidationMessage`или и того, и другого.</span><span class="sxs-lookup"><span data-stu-id="6260d-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="6260d-149">В следующем примере показана страница, на которой показаны эти шаги.</span><span class="sxs-lookup"><span data-stu-id="6260d-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="6260d-150">Чтобы узнать, как работает проверка, запустите эту страницу и намеренно выполните ошибки.</span><span class="sxs-lookup"><span data-stu-id="6260d-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="6260d-151">Например, вот как выглядит страница, если вы забыли ввести название курса, если ввести и ввести недопустимую дату:</span><span class="sxs-lookup"><span data-stu-id="6260d-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![Ошибки проверки на странице, подготовленной для просмотра](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="6260d-153">Добавление клиентской проверки</span><span class="sxs-lookup"><span data-stu-id="6260d-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="6260d-154">По умолчанию вводимые пользователем данные проверяются после того, как пользователи отправляют страницу — то есть проверка выполняется в коде сервера.</span><span class="sxs-lookup"><span data-stu-id="6260d-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="6260d-155">Недостаток этого подхода заключается в том, что пользователи не узнают, что они сделали ошибку до отправки страницы.</span><span class="sxs-lookup"><span data-stu-id="6260d-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="6260d-156">Если форма является длинной или сложной, отчеты об ошибках могут быть неудобными для пользователя только после отправки страницы.</span><span class="sxs-lookup"><span data-stu-id="6260d-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="6260d-157">Вы можете добавить поддержку для выполнения проверки в клиентском скрипте.</span><span class="sxs-lookup"><span data-stu-id="6260d-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="6260d-158">В этом случае проверка выполняется по мере работы пользователей в браузере.</span><span class="sxs-lookup"><span data-stu-id="6260d-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="6260d-159">Например, предположим, что значение должно быть целым числом.</span><span class="sxs-lookup"><span data-stu-id="6260d-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="6260d-160">Если пользователь вводит нецелочисленное значение, сообщение об ошибке выводится сразу после того, как пользователь покидает поле ввода.</span><span class="sxs-lookup"><span data-stu-id="6260d-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="6260d-161">Пользователи получают немедленную обратную связь, которая удобна для них.</span><span class="sxs-lookup"><span data-stu-id="6260d-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="6260d-162">Проверка на основе клиента может также сократить число попыток пользователя отправить форму для исправления нескольких ошибок.</span><span class="sxs-lookup"><span data-stu-id="6260d-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="6260d-163">Даже если используется проверка на стороне клиента, проверка всегда выполняется в коде сервера.</span><span class="sxs-lookup"><span data-stu-id="6260d-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="6260d-164">Выполнение проверки в коде сервера — это мера безопасности, если пользователи обходят проверку на основе клиента.</span><span class="sxs-lookup"><span data-stu-id="6260d-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>

1. <span data-ttu-id="6260d-165">Зарегистрируйте следующие библиотеки JavaScript на странице:</span><span class="sxs-lookup"><span data-stu-id="6260d-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="6260d-166">Две библиотеки доступны для загрузки из сети доставки содержимого (CDN), поэтому они не обязательно должны находиться на компьютере или сервере.</span><span class="sxs-lookup"><span data-stu-id="6260d-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="6260d-167">Однако необходимо иметь локальную копию *jQuery. Validate. unobtrusive. js*.</span><span class="sxs-lookup"><span data-stu-id="6260d-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="6260d-168">Если вы еще не работаете с шаблоном WebMatrix (например, **начальным сайтом** ), включающим библиотеку, создайте сайт веб-страниц, основанный на **начальном сайте**.</span><span class="sxs-lookup"><span data-stu-id="6260d-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="6260d-169">Затем скопируйте *JS* -файл на текущий сайт.</span><span class="sxs-lookup"><span data-stu-id="6260d-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="6260d-170">В разметке для каждого проверяемого элемента добавьте вызов `Validation.For(field)`.</span><span class="sxs-lookup"><span data-stu-id="6260d-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="6260d-171">Этот метод выдает атрибуты, используемые при проверке на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="6260d-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="6260d-172">(Вместо того, чтобы выдавать фактический код JavaScript, метод выдает такие атрибуты, как `data-val-...`.</span><span class="sxs-lookup"><span data-stu-id="6260d-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="6260d-173">Эти атрибуты поддерживают ненавязчивую проверку клиента, которая использует jQuery для выполнения работы.)</span><span class="sxs-lookup"><span data-stu-id="6260d-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="6260d-174">На следующей странице показано, как добавить функции проверки клиента в приведенный выше пример.</span><span class="sxs-lookup"><span data-stu-id="6260d-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="6260d-175">Не все проверки выполняются на клиенте.</span><span class="sxs-lookup"><span data-stu-id="6260d-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="6260d-176">В частности, проверка типа данных (целое число, Дата и т. д.) не выполняется на клиенте.</span><span class="sxs-lookup"><span data-stu-id="6260d-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="6260d-177">Следующие проверки работают и на клиенте, и на сервере:</span><span class="sxs-lookup"><span data-stu-id="6260d-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="6260d-178">В этом примере тест для допустимой даты не будет работать в клиентском коде.</span><span class="sxs-lookup"><span data-stu-id="6260d-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="6260d-179">Однако тест будет выполняться в коде сервера.</span><span class="sxs-lookup"><span data-stu-id="6260d-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="6260d-180">Ошибки проверки форматирования</span><span class="sxs-lookup"><span data-stu-id="6260d-180">Formatting Validation Errors</span></span>

<span data-ttu-id="6260d-181">Вы можете управлять отображением ошибок проверки, определив классы CSS, которые имеют следующие зарезервированные имена:</span><span class="sxs-lookup"><span data-stu-id="6260d-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="6260d-182">`field-validation-error`.</span><span class="sxs-lookup"><span data-stu-id="6260d-182">`field-validation-error`.</span></span> <span data-ttu-id="6260d-183">Определяет выходные данные метода `Html.ValidationMessage` при отображении ошибки.</span><span class="sxs-lookup"><span data-stu-id="6260d-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="6260d-184">`field-validation-valid`.</span><span class="sxs-lookup"><span data-stu-id="6260d-184">`field-validation-valid`.</span></span> <span data-ttu-id="6260d-185">Определяет выходные данные метода `Html.ValidationMessage` при отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="6260d-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="6260d-186">`input-validation-error`.</span><span class="sxs-lookup"><span data-stu-id="6260d-186">`input-validation-error`.</span></span> <span data-ttu-id="6260d-187">Определяет, как `<input>` подготавливать элементы при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="6260d-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="6260d-188">(Например, с помощью этого класса можно задать цвет фона &lt;входного элемента&gt;, который имеет другой цвет, если его значение недопустимо.) Этот класс CSS используется только во время проверки клиента (в веб-страницы ASP.NET 2).</span><span class="sxs-lookup"><span data-stu-id="6260d-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="6260d-189">`input-validation-valid`.</span><span class="sxs-lookup"><span data-stu-id="6260d-189">`input-validation-valid`.</span></span> <span data-ttu-id="6260d-190">Определяет внешний вид элементов `<input>` при отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="6260d-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="6260d-191">`validation-summary-errors`.</span><span class="sxs-lookup"><span data-stu-id="6260d-191">`validation-summary-errors`.</span></span> <span data-ttu-id="6260d-192">Определяет выходные данные метода `Html.ValidationSummary`, в котором отображается список ошибок.</span><span class="sxs-lookup"><span data-stu-id="6260d-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="6260d-193">`validation-summary-valid`.</span><span class="sxs-lookup"><span data-stu-id="6260d-193">`validation-summary-valid`.</span></span> <span data-ttu-id="6260d-194">Определяет выходные данные метода `Html.ValidationSummary` при отсутствии ошибок.</span><span class="sxs-lookup"><span data-stu-id="6260d-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="6260d-195">В следующем блоке `<style>` показаны правила для условий ошибки.</span><span class="sxs-lookup"><span data-stu-id="6260d-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="6260d-196">Если включить этот блок стиля в примеры страниц, описанные ранее в этой статье, то отображение ошибок будет выглядеть, как на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="6260d-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![Ошибки проверки, использующие классы стилей CSS](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="6260d-198">Если клиентская проверка не используется в веб-страницы ASP.NET 2, классы CSS для элементов `<input>` (`input-validation-error` и `input-validation-valid` не имеют никакого влияния.</span><span class="sxs-lookup"><span data-stu-id="6260d-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>

### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="6260d-199">Статическое и динамическое отображение ошибок</span><span class="sxs-lookup"><span data-stu-id="6260d-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="6260d-200">Правила CSS поставляются в виде пар, таких как `validation-summary-errors` и `validation-summary-valid`.</span><span class="sxs-lookup"><span data-stu-id="6260d-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="6260d-201">Эти пары позволяют определять правила для обоих условий: условие ошибки и условие "нормальное (не ошибка)".</span><span class="sxs-lookup"><span data-stu-id="6260d-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="6260d-202">Важно понимать, что разметка для отображения ошибок всегда отображается, даже если ошибок нет.</span><span class="sxs-lookup"><span data-stu-id="6260d-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="6260d-203">Например, если на странице имеется `Html.ValidationSummary` метод в разметке, то источник страницы будет содержать следующую разметку, даже если страница запрашивается в первый раз:</span><span class="sxs-lookup"><span data-stu-id="6260d-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="6260d-204">Иными словами, метод `Html.ValidationSummary` всегда отображает элемент `<div>` и список, даже если список ошибок пуст.</span><span class="sxs-lookup"><span data-stu-id="6260d-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="6260d-205">Аналогичным образом, метод `Html.ValidationMessage` всегда отображает элемент `<span>` в качестве заполнителя для ошибки отдельного поля, даже если нет ошибки.</span><span class="sxs-lookup"><span data-stu-id="6260d-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="6260d-206">В некоторых ситуациях отображение сообщения об ошибке может вызвать перекомпоновку страницы и может вызвать перемещение элементов на странице.</span><span class="sxs-lookup"><span data-stu-id="6260d-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="6260d-207">Правила CSS, которые заканчиваются `-valid` позволяют определить макет, который может помочь предотвратить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="6260d-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="6260d-208">Например, можно определить, `field-validation-error` и `field-validation-valid` оба имеют одинаковый фиксированный размер.</span><span class="sxs-lookup"><span data-stu-id="6260d-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="6260d-209">Таким образом, область отображения для поля является статической и не будет изменяться при отображении сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="6260d-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="6260d-210">Проверка данных, которые не приходят непосредственно от пользователей</span><span class="sxs-lookup"><span data-stu-id="6260d-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="6260d-211">Иногда необходимо проверить сведения, которые не поступают непосредственно из HTML-формы.</span><span class="sxs-lookup"><span data-stu-id="6260d-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="6260d-212">Типичным примером является страница, в которой значение передается в строке запроса, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="6260d-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="6260d-213">В этом случае необходимо убедиться, что значение, передаваемое на страницу (здесь 1022 для значения `classid`), является допустимым.</span><span class="sxs-lookup"><span data-stu-id="6260d-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="6260d-214">Для выполнения этой проверки нельзя напрямую использовать вспомогательный метод `Validation`.</span><span class="sxs-lookup"><span data-stu-id="6260d-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="6260d-215">Однако можно использовать другие функции системы проверки, например возможность отображать сообщения об ошибках проверки.</span><span class="sxs-lookup"><span data-stu-id="6260d-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6260d-216">**Важно!** Всегда проверяйте значения, получаемые из *любого* источника, включая значения полей форм, значения строк запросов и значения файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="6260d-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="6260d-217">Пользователям легко изменить эти значения (возможно, для вредоносных целей).</span><span class="sxs-lookup"><span data-stu-id="6260d-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="6260d-218">Поэтому необходимо проверить эти значения, чтобы защитить приложение.</span><span class="sxs-lookup"><span data-stu-id="6260d-218">So you must check these values in order to protect your application.</span></span>

<span data-ttu-id="6260d-219">В следующем примере показано, как можно проверить значение, передаваемое в строку запроса.</span><span class="sxs-lookup"><span data-stu-id="6260d-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="6260d-220">Код проверяет, что значение не пусто и является целым числом.</span><span class="sxs-lookup"><span data-stu-id="6260d-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="6260d-221">Обратите внимание, что тест выполняется, если запрос не является отправкой формы (`if(!IsPost)`).</span><span class="sxs-lookup"><span data-stu-id="6260d-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="6260d-222">Этот тест будет пройден при первом запросе страницы, но не в том случае, если запрос является отправкой формы.</span><span class="sxs-lookup"><span data-stu-id="6260d-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="6260d-223">Чтобы отобразить эту ошибку, можно добавить ошибку в список ошибок проверки, вызвав `Validation.AddFormError("message")`.</span><span class="sxs-lookup"><span data-stu-id="6260d-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="6260d-224">Если страница содержит вызов метода `Html.ValidationSummary`, отображается ошибка, аналогично ошибке проверки ввода пользователем.</span><span class="sxs-lookup"><span data-stu-id="6260d-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="6260d-225">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6260d-225">Additional Resources</span></span>

[<span data-ttu-id="6260d-226">Работа с HTML-формами на веб-страницы ASP.NET сайтах</span><span class="sxs-lookup"><span data-stu-id="6260d-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
