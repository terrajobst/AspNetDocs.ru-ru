---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Общие сведения о веб-программировании ASP.NET с использованиемC#синтаксиса Razor () | Документация Майкрософт
author: Rick-Anderson
description: Эта глава содержит общие сведения о программировании с помощью веб-страницы ASP.NET синтаксис Razor. ASP.NET — Технология Майкрософт для запуска динамического веб-приложения PA...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564887"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="978a3-104">Общие сведения о веб-программировании ASP.NET с использованиемC#синтаксиса Razor ()</span><span class="sxs-lookup"><span data-stu-id="978a3-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="978a3-105">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="978a3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="978a3-106">В этой статье приводятся общие сведения о программировании с помощью веб-страницы ASP.NET синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="978a3-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="978a3-107">ASP.NET — это технология корпорации Майкрософт для запуска динамических веб-страниц на веб-серверах.</span><span class="sxs-lookup"><span data-stu-id="978a3-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="978a3-108">В этой статье рассматривается использование языка C# программирования.</span><span class="sxs-lookup"><span data-stu-id="978a3-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="978a3-109">**Что вы**узнаете:</span><span class="sxs-lookup"><span data-stu-id="978a3-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="978a3-110">8 лучших советов по программированию для начинающих веб-страницы ASP.NET с помощью синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="978a3-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="978a3-111">Основные понятия программирования, которые вам понадобятся.</span><span class="sxs-lookup"><span data-stu-id="978a3-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="978a3-112">Что ASP.NET серверный код и синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="978a3-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="978a3-113">Версии программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="978a3-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="978a3-114">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="978a3-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="978a3-115">Этот учебник также работает с веб-страницы ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="978a3-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="978a3-116">8 лучших советов по программированию</span><span class="sxs-lookup"><span data-stu-id="978a3-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="978a3-117">В этом разделе приведено несколько советов, которые необходимо знать при написании кода сервера ASP.NET с помощью синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="978a3-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="978a3-118">Синтаксис Razor основан на языке C# программирования, и это тот язык, который чаще всего используется с веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="978a3-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="978a3-119">Однако синтаксис Razor также поддерживает язык Visual Basic и все, что вы видите, можно также сделать в Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="978a3-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="978a3-120">Дополнительные сведения см. в приложении [Visual Basic языке и синтаксисе](https://go.microsoft.com/fwlink/?LinkId=202908).</span><span class="sxs-lookup"><span data-stu-id="978a3-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="978a3-121">Дополнительные сведения о большинстве этих методов программирования см. Далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="978a3-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="978a3-122">1. Вы добавляете код на страницу с помощью символа @.</span><span class="sxs-lookup"><span data-stu-id="978a3-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="978a3-123">`@` символ начинается со встроенных выражений, блоков одиночных инструкций и многооператорных блоков:</span><span class="sxs-lookup"><span data-stu-id="978a3-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="978a3-124">Эти инструкции выглядят так, как если бы страница выполнялась в браузере:</span><span class="sxs-lookup"><span data-stu-id="978a3-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor — Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="978a3-126">**Кодировка HTML**</span><span class="sxs-lookup"><span data-stu-id="978a3-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="978a3-127">При отображении содержимого на странице с помощью `@` символа, как в предыдущих примерах, ASP.NET HTML кодирует выходные данные.</span><span class="sxs-lookup"><span data-stu-id="978a3-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="978a3-128">Это заменяет зарезервированные символы HTML (например, `<` и `>` и `&`) кодами, которые позволяют отображать символы в виде символов на веб-странице, а не интерпретировать их как теги HTML или сущности.</span><span class="sxs-lookup"><span data-stu-id="978a3-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="978a3-129">Без кодирования HTML выходные данные из кода сервера могут отображаться неправильно, и может представлять угрозу безопасности страницы.</span><span class="sxs-lookup"><span data-stu-id="978a3-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="978a3-130">Если ваша цель — вывод HTML-разметки, которая отображает теги как разметку (например `<p></p>` для абзаца или `<em></em>`, чтобы подчеркнуть текст), см. раздел [Объединение текста, разметки и кода в блоках кода](#BM_CombiningTextMarkupAndCode) ниже в этой статье.</span><span class="sxs-lookup"><span data-stu-id="978a3-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="978a3-131">Дополнительные сведения о кодировке HTML см. в статье [Работа с формами](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="978a3-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="978a3-132">2. блоки кода заключены в фигурные скобки</span><span class="sxs-lookup"><span data-stu-id="978a3-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="978a3-133">*Блок кода* включает один или несколько операторов кода и заключен в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="978a3-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="978a3-134">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="978a3-134">The result displayed in a browser:</span></span>

![Razor — Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="978a3-136">3. внутри блока все операторы кода завершаются точкой с запятой</span><span class="sxs-lookup"><span data-stu-id="978a3-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="978a3-137">Внутри блока кода Каждая полная инструкция Code должна заканчиваться точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="978a3-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="978a3-138">Встроенные выражения не заканчиваются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="978a3-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="978a3-139">4. переменные используются для хранения значений</span><span class="sxs-lookup"><span data-stu-id="978a3-139">4. You use variables to store values</span></span>

<span data-ttu-id="978a3-140">Значения можно хранить в *переменной*, включая строки, числа и даты и т. д. Новую переменную можно создать с помощью ключевого слова `var`.</span><span class="sxs-lookup"><span data-stu-id="978a3-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="978a3-141">Значения переменных можно вставлять непосредственно на странице с помощью `@`.</span><span class="sxs-lookup"><span data-stu-id="978a3-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="978a3-142">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="978a3-142">The result displayed in a browser:</span></span>

![Razor — Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="978a3-144">5. строковые литеральные значения заключаются в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="978a3-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="978a3-145">*Строка* представляет собой последовательность символов, обрабатываемых как текст.</span><span class="sxs-lookup"><span data-stu-id="978a3-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="978a3-146">Чтобы указать строку, заключите ее в двойные кавычки:</span><span class="sxs-lookup"><span data-stu-id="978a3-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="978a3-147">Если строка, которую требуется отобразить, содержит символ обратной косой черты (`\`) или двойные кавычки (`"`), используйте *Буквальный строковый литерал* с префиксом оператора `@`.</span><span class="sxs-lookup"><span data-stu-id="978a3-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="978a3-148">(В C#символ \ имеет специальное значение, если не используется Буквальный строковый литерал.)</span><span class="sxs-lookup"><span data-stu-id="978a3-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="978a3-149">Чтобы внедрить двойные кавычки, используйте Буквальный строковый литерал и повторите кавычки:</span><span class="sxs-lookup"><span data-stu-id="978a3-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="978a3-150">Вот результат использования обоих примеров на странице:</span><span class="sxs-lookup"><span data-stu-id="978a3-150">Here's the result of using both of these examples in a page:</span></span>

![Razor — Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="978a3-152">Обратите внимание, что символ `@` используется как для пометки буквальных строковых C# литералов в, так и для пометки кода на страницах ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="978a3-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="978a3-153">6. код учитывает регистр</span><span class="sxs-lookup"><span data-stu-id="978a3-153">6. Code is case sensitive</span></span>

<span data-ttu-id="978a3-154">В C#ключевые слова (такие как `var`, `true`и `if`) и имена переменных чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="978a3-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="978a3-155">Следующие строки кода создают две различные переменные: `lastName` и `LastName.`</span><span class="sxs-lookup"><span data-stu-id="978a3-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="978a3-156">Если вы объявили переменную как `var lastName = "Smith";` и пытаетесь сослаться на эту переменную на странице как `@LastName`, вы получите значение `"Jones"` вместо `"Smith"`.</span><span class="sxs-lookup"><span data-stu-id="978a3-156">If you declare a variable as `var lastName = "Smith";` and try to reference that variable in your page as `@LastName`, you would get the value `"Jones"` instead of `"Smith"`.</span></span>

> [!NOTE]
> <span data-ttu-id="978a3-157">В Visual Basic ключевые слова и переменные *не* учитывают регистр.</span><span class="sxs-lookup"><span data-stu-id="978a3-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="978a3-158">7. большая часть кода включает объекты</span><span class="sxs-lookup"><span data-stu-id="978a3-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="978a3-159">*Объект* представляет вещь, которую можно программировать с &#8212; помощью страницы, текстового поля, файла, изображения, веб-запроса, сообщения электронной почты, записи клиента (строки базы данных) и т. д. Объекты имеют свойства, описывающие их характеристики, а также возможность чтения или &#8212; изменения объекта текстового поля имеет свойство `Text` (в других случаях), объект запроса имеет свойство `Url`, сообщение электронной почты имеет свойство `From`, а объект Customer имеет свойство `FirstName`.</span><span class="sxs-lookup"><span data-stu-id="978a3-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="978a3-160">Объекты также имеют методы, которые являются &quot;командами&quot; они могут выполняться.</span><span class="sxs-lookup"><span data-stu-id="978a3-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="978a3-161">К примерам относятся метод `Save` файлового объекта, метод `Rotate` объекта изображения и метод `Send` объекта сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="978a3-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="978a3-162">Часто приходится работать с объектом `Request`, который предоставляет сведения, такие как значения текстовых полей (полей формы) на странице, тип браузера, который сделал запрос, URL-адрес страницы, удостоверение пользователя и т. д. В следующем примере показано, как получить доступ к свойствам объекта `Request` и вызвать метод `MapPath` объекта `Request`, который предоставляет абсолютный путь к странице на сервере:</span><span class="sxs-lookup"><span data-stu-id="978a3-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="978a3-163">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="978a3-163">The result displayed in a browser:</span></span>

![Razor — Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="978a3-165">8. можно написать код, который принимает решения</span><span class="sxs-lookup"><span data-stu-id="978a3-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="978a3-166">Ключевой функцией динамических веб-страниц является то, что вы можете определить, что делать на основе условий.</span><span class="sxs-lookup"><span data-stu-id="978a3-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="978a3-167">Самый распространенный способ сделать это — с помощью оператора `if` (и необязательной инструкции `else`).</span><span class="sxs-lookup"><span data-stu-id="978a3-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="978a3-168">`if(IsPost)` инструкции — это сокращенный способ написания `if(IsPost == true)`.</span><span class="sxs-lookup"><span data-stu-id="978a3-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="978a3-169">Наряду с инструкциями `if` существует множество способов проверки условий, повторных блоков кода и т. д., которые описаны далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="978a3-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="978a3-170">Результат, отображаемый в браузере (после нажатия кнопки **Отправить**):</span><span class="sxs-lookup"><span data-stu-id="978a3-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor — Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="978a3-172">Методы HTTP GET и POST и свойство POST</span><span class="sxs-lookup"><span data-stu-id="978a3-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="978a3-173">Протокол, используемый для веб-страниц (HTTP), поддерживает очень ограниченное количество методов (глаголов), которые используются для выполнения запросов к серверу.</span><span class="sxs-lookup"><span data-stu-id="978a3-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="978a3-174">Двумя наиболее распространенными являются GET, который используется для чтения страницы, и POST, который используется для отправки страницы.</span><span class="sxs-lookup"><span data-stu-id="978a3-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="978a3-175">В общем случае при первом запросе страницы пользователем страница запрашивается с помощью GET.</span><span class="sxs-lookup"><span data-stu-id="978a3-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="978a3-176">Если пользователь заполняет форму, а затем нажимает кнопку Отправить, браузер отправляет запрос POST на сервер.</span><span class="sxs-lookup"><span data-stu-id="978a3-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="978a3-177">В веб-программировании часто бывает полезно определить, запрашивается ли страница как GET или AS POST, чтобы вы узнали, как обрабатывать страницу.</span><span class="sxs-lookup"><span data-stu-id="978a3-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="978a3-178">В веб-страницы ASP.NET можно использовать свойство `IsPost`, чтобы определить, является ли запрос сообщением GET или POST.</span><span class="sxs-lookup"><span data-stu-id="978a3-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="978a3-179">Если запрос является POST, свойство `IsPost` возвратит значение true, и вы можете выполнять такие действия, как чтение значений текстовых полей в форме.</span><span class="sxs-lookup"><span data-stu-id="978a3-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="978a3-180">Во многих примерах вы увидите, как обрабатывать страницу по-разному в зависимости от значения `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="978a3-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="978a3-181">Простой пример кода</span><span class="sxs-lookup"><span data-stu-id="978a3-181">A Simple Code Example</span></span>

<span data-ttu-id="978a3-182">В этой процедуре показано, как создать страницу, на которой показаны основные методики программирования.</span><span class="sxs-lookup"><span data-stu-id="978a3-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="978a3-183">В этом примере создается страница, позволяющая пользователям вводить два числа, затем добавляет их и отображает результат.</span><span class="sxs-lookup"><span data-stu-id="978a3-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="978a3-184">В редакторе создайте новый файл и назовите его *подставлял. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="978a3-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="978a3-185">Скопируйте приведенный ниже код и разметку на страницу, заменив все, что уже есть на странице.</span><span class="sxs-lookup"><span data-stu-id="978a3-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="978a3-186">Обратите внимание на некоторые моменты.</span><span class="sxs-lookup"><span data-stu-id="978a3-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="978a3-187">Символ `@` запускает первый блок кода на странице и перед переменной `totalMessage`, внедренной в нижнюю часть страницы.</span><span class="sxs-lookup"><span data-stu-id="978a3-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="978a3-188">Блок в верхней части страницы заключен в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="978a3-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="978a3-189">В блоке в начале все строки заканчиваются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="978a3-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="978a3-190">Переменные `total`, `num1`, `num2`и `totalMessage` хранят несколько чисел и строку.</span><span class="sxs-lookup"><span data-stu-id="978a3-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="978a3-191">Литеральное строковое значение, присваиваемое переменной `totalMessage`, заключено в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="978a3-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="978a3-192">Так как в коде учитывается регистр, то, когда в нижней части страницы используется `totalMessage` переменная, ее имя должно соответствовать переменной в верхней части.</span><span class="sxs-lookup"><span data-stu-id="978a3-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="978a3-193">Выражение `num1.AsInt() + num2.AsInt()` показывает, как работать с объектами и методами.</span><span class="sxs-lookup"><span data-stu-id="978a3-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="978a3-194">Метод `AsInt` для каждой переменной преобразует строку, введенную пользователем, в число (целое число), чтобы можно было выполнять арифметические действия.</span><span class="sxs-lookup"><span data-stu-id="978a3-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="978a3-195">Тег `<form>` содержит атрибут `method="post"`.</span><span class="sxs-lookup"><span data-stu-id="978a3-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="978a3-196">Это указывает, что при нажатии пользователем кнопки **Добавить**страница будет отправлена на сервер с помощью метода HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="978a3-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="978a3-197">При отправке страницы `if(IsPost)` тест оценивается как true и выполняется условный код, отображая результат сложения чисел.</span><span class="sxs-lookup"><span data-stu-id="978a3-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="978a3-198">Сохраните страницу и запустите ее в браузере.</span><span class="sxs-lookup"><span data-stu-id="978a3-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="978a3-199">(Перед выполнением страницы убедитесь, что она выбрана в рабочей области **файлы** .) Введите два целых числа и нажмите кнопку " **Добавить** ".</span><span class="sxs-lookup"><span data-stu-id="978a3-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor — Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="978a3-201">Основные понятия программирования</span><span class="sxs-lookup"><span data-stu-id="978a3-201">Basic Programming Concepts</span></span>

<span data-ttu-id="978a3-202">В этой статье представлен обзор веб-программирования ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="978a3-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="978a3-203">Это не исчерпывающее исследование, а краткий обзор наиболее часто используемых концепций программирования.</span><span class="sxs-lookup"><span data-stu-id="978a3-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="978a3-204">Несмотря на это, он охватывает почти все, что потребуется для начала работы с веб-страницы ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="978a3-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="978a3-205">Но сначала немного технический фон.</span><span class="sxs-lookup"><span data-stu-id="978a3-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="978a3-206">Синтаксис Razor, серверный код и ASP.NET</span><span class="sxs-lookup"><span data-stu-id="978a3-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="978a3-207">Синтаксис Razor — это простой синтаксис программирования для внедрения кода на основе сервера на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="978a3-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="978a3-208">На веб-странице, использующей синтаксис Razor, существует два типа содержимого: содержимое клиента и серверный код.</span><span class="sxs-lookup"><span data-stu-id="978a3-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="978a3-209">Содержимое клиента — это то, что вы используете на веб-страницах: разметка HTML (элементы), сведения о стиле, такие как CSS, возможно, некоторые клиентские сценарии, такие как JavaScript, и обычный текст.</span><span class="sxs-lookup"><span data-stu-id="978a3-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="978a3-210">Синтаксис Razor позволяет добавлять серверный код в содержимое этого клиента.</span><span class="sxs-lookup"><span data-stu-id="978a3-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="978a3-211">Если на странице имеется серверный код, то перед отправкой страницы в браузер сервер сначала выполняет этот код.</span><span class="sxs-lookup"><span data-stu-id="978a3-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="978a3-212">При запуске на сервере код может выполнять задачи, которые могут быть гораздо более сложными для использования только содержимого клиента, например для доступа к серверным базам данных.</span><span class="sxs-lookup"><span data-stu-id="978a3-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="978a3-213">Что более важно, серверный код может динамически создавать &#8212; клиентское содержимое, которое может создать разметку HTML или другое содержимое на лету, а затем отправить его в браузер вместе со статическим HTML-кодом, который может содержать страница.</span><span class="sxs-lookup"><span data-stu-id="978a3-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="978a3-214">С точки зрения браузера содержимое клиента, созданное кодом сервера, отличается от содержимого любого другого клиентского содержимого.</span><span class="sxs-lookup"><span data-stu-id="978a3-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="978a3-215">Как вы уже видели, необходимый серверный код довольно прост.</span><span class="sxs-lookup"><span data-stu-id="978a3-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="978a3-216">Веб-страницы ASP.NET, содержащие синтаксис Razor, имеют специальное расширение файла ( *. cshtml* или *. vbhtml*).</span><span class="sxs-lookup"><span data-stu-id="978a3-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="978a3-217">Сервер распознает эти расширения, выполняет код, помеченный синтаксис Razor, а затем отправляет страницу в браузер.</span><span class="sxs-lookup"><span data-stu-id="978a3-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="978a3-218">Где ASP.NET помещается в?</span><span class="sxs-lookup"><span data-stu-id="978a3-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="978a3-219">Синтаксис Razor основан на технологии корпорации Майкрософт, именуемой ASP.NET, которая, в свою очередь, основана на Microsoft .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="978a3-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="978a3-220">The.NET Framework — это обширная комплексная платформа программирования от корпорации Майкрософт для разработки практически любого типа компьютерных приложений.</span><span class="sxs-lookup"><span data-stu-id="978a3-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="978a3-221">ASP.NET является частью .NET Framework, специально предназначенной для создания веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="978a3-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="978a3-222">Разработчики использовали ASP.NET для создания множества веб-сайтов самого большого и наибольшего трафика в мире.</span><span class="sxs-lookup"><span data-stu-id="978a3-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="978a3-223">(Каждый раз, когда вы видите имя файла Extension *. aspx* как часть URL-адреса сайта, вы узнаете, что сайт был написан с помощью ASP.NET.)</span><span class="sxs-lookup"><span data-stu-id="978a3-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="978a3-224">Синтаксис Razor предоставляет все возможности ASP.NET, но использование упрощенного синтаксиса упрощает изучение, если вы являетесь новичком и что повышает продуктивность работы, если вы эксперт.</span><span class="sxs-lookup"><span data-stu-id="978a3-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="978a3-225">Несмотря на то, что этот синтаксис прост в использовании, его семейство отношений с ASP.NET и .NET Framework означает, что веб-сайты становятся более сложными, вы можете воспользоваться преимуществами более крупных платформ.</span><span class="sxs-lookup"><span data-stu-id="978a3-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor — Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="978a3-227">**Классы и экземпляры**</span><span class="sxs-lookup"><span data-stu-id="978a3-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="978a3-228">ASP.NET Server Code использует объекты, которые, в свою очередь, основаны на идее классов.</span><span class="sxs-lookup"><span data-stu-id="978a3-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="978a3-229">Класс является определением или шаблоном для объекта.</span><span class="sxs-lookup"><span data-stu-id="978a3-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="978a3-230">Например, приложение может содержать класс `Customer`, определяющий свойства и методы, необходимые для любого объекта клиента.</span><span class="sxs-lookup"><span data-stu-id="978a3-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="978a3-231">Когда приложение должно работать с фактическими сведениями о клиентах, оно создает экземпляр (или *экземпляр*) объекта Customer.</span><span class="sxs-lookup"><span data-stu-id="978a3-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="978a3-232">Каждый отдельный клиент является отдельным экземпляром класса `Customer`.</span><span class="sxs-lookup"><span data-stu-id="978a3-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="978a3-233">Каждый экземпляр поддерживает одни и те же свойства и методы, но значения свойств для каждого экземпляра обычно отличаются, так как каждый объект Customer является уникальным.</span><span class="sxs-lookup"><span data-stu-id="978a3-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="978a3-234">В одном объекте Customer свойство `LastName` может иметь значение Smith; в другом объекте Customer свойство `LastName` может иметь значение "Jones".</span><span class="sxs-lookup"><span data-stu-id="978a3-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="978a3-235">Точно так же любая отдельная веб-страница на сайте является объектом `Page`, который является экземпляром класса `Page`.</span><span class="sxs-lookup"><span data-stu-id="978a3-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="978a3-236">Кнопка на странице — это `Button` объект, являющийся экземпляром класса `Button` и т. д.</span><span class="sxs-lookup"><span data-stu-id="978a3-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="978a3-237">Каждый экземпляр имеет свои собственные характеристики, но все они основаны на том, что указано в определении класса объекта.</span><span class="sxs-lookup"><span data-stu-id="978a3-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="978a3-238">Базовый синтаксис</span><span class="sxs-lookup"><span data-stu-id="978a3-238">Basic Syntax</span></span>

<span data-ttu-id="978a3-239">Ранее вы увидели простой пример создания веб-страницы ASP.NET страницы, а также способ добавления серверного кода в разметку HTML.</span><span class="sxs-lookup"><span data-stu-id="978a3-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="978a3-240">Здесь вы узнаете об основах написания ASP.NET Server Code с помощью синтаксис Razor &#8212; , то есть правил языка программирования.</span><span class="sxs-lookup"><span data-stu-id="978a3-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="978a3-241">При работе с программированием (особенно если вы использовали C, C++, C#, Visual Basic или JavaScript), многие из которых вы прочитаете здесь, будут знакомы.</span><span class="sxs-lookup"><span data-stu-id="978a3-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="978a3-242">Возможно, вам потребуется ознакомиться только с тем, как серверный код добавляется к разметке в *CSHTML* -файлах.</span><span class="sxs-lookup"><span data-stu-id="978a3-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="978a3-243">Объединение текста, разметки и кода в блоках кода</span><span class="sxs-lookup"><span data-stu-id="978a3-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="978a3-244">В блоках кода сервера часто требуется выводить текст или разметку (или и то, и другое) на страницу.</span><span class="sxs-lookup"><span data-stu-id="978a3-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="978a3-245">Если блок кода сервера содержит текст, который не является кодом и, вместо этого, он должен быть отображен как есть, ASP.NET должен иметь возможность отличать этот текст от кода.</span><span class="sxs-lookup"><span data-stu-id="978a3-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="978a3-246">Для этого можно использовать следующие способы.</span><span class="sxs-lookup"><span data-stu-id="978a3-246">There are several ways to do this.</span></span>

- <span data-ttu-id="978a3-247">Заключите текст в HTML-элемент, например `<p></p>` или `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="978a3-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="978a3-248">Элемент HTML может включать текст, дополнительные HTML-элементы и выражения серверного кода.</span><span class="sxs-lookup"><span data-stu-id="978a3-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="978a3-249">Когда ASP.NET видит открывающий HTML-тег (например, `<p>`), он отображает все, включая элемент и его содержимое, как в браузере, устраняя при этом выражения серверного кода.</span><span class="sxs-lookup"><span data-stu-id="978a3-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="978a3-250">Используйте оператор `@:` или элемент `<text>`.</span><span class="sxs-lookup"><span data-stu-id="978a3-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="978a3-251">`@:` выводит одну строку содержимого, содержащую обычный текст или несовпадающие теги HTML; элемент `<text>` включает несколько строк для вывода.</span><span class="sxs-lookup"><span data-stu-id="978a3-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="978a3-252">Эти параметры полезны, если не нужно отображать HTML-элемент как часть выходных данных.</span><span class="sxs-lookup"><span data-stu-id="978a3-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="978a3-253">Если требуется выводить несколько строк текста или несовпадающих HTML-тегов, можно указать в каждой строке `@:`или заключить строку в элемент `<text>`.</span><span class="sxs-lookup"><span data-stu-id="978a3-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="978a3-254">Как и оператор `@:`, Теги`<text>` используются ASP.NET для распознавания текстового содержимого и никогда не подготавливаются к просмотру в выходных данных страницы.</span><span class="sxs-lookup"><span data-stu-id="978a3-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="978a3-255">Первый пример повторяет предыдущий пример, но использует одну пару тегов `<text>`, чтобы заключить текст в отрисовку.</span><span class="sxs-lookup"><span data-stu-id="978a3-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="978a3-256">Во втором примере Теги `<text>` и `</text>` заключаются в три строки, все из которых содержат неавтономный текст и непарные теги HTML (`<br />`) вместе с серверным кодом и соответствующими тегами HTML.</span><span class="sxs-lookup"><span data-stu-id="978a3-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="978a3-257">Опять же, можно также предшествовать каждой строке отдельно с помощью оператора `@:`. в любом случае это работает.</span><span class="sxs-lookup"><span data-stu-id="978a3-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="978a3-258">При выводе текста, как показано в этом &#8212; разделе, с помощью элемента html, `@:` оператор или `<text>` элемент &#8212; ASP.NET не кодирует выходные данные в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="978a3-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="978a3-259">(Как отмечалось ранее, ASP.NET кодирует выходные данные выражений серверного кода и серверных блоков кода, которым предшествуют `@`, за исключением особых случаев, указанных в этом разделе.)</span><span class="sxs-lookup"><span data-stu-id="978a3-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="978a3-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="978a3-260">Whitespace</span></span>

<span data-ttu-id="978a3-261">Лишние пробелы в операторе (и вне строкового литерала) не влияют на инструкцию:</span><span class="sxs-lookup"><span data-stu-id="978a3-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="978a3-262">Разрыв строки в операторе не влияет на инструкцию, и можно заключить инструкции для удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="978a3-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="978a3-263">Следующие инструкции равнозначны:</span><span class="sxs-lookup"><span data-stu-id="978a3-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="978a3-264">Однако нельзя заключить строку в середину строкового литерала.</span><span class="sxs-lookup"><span data-stu-id="978a3-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="978a3-265">Следующий пример не работает:</span><span class="sxs-lookup"><span data-stu-id="978a3-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="978a3-266">Чтобы объединить длинную строку, которая является оболочкой для нескольких строк, например приведенного выше кода, существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="978a3-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="978a3-267">Можно использовать оператор объединения (`+`), который будет приведен далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="978a3-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="978a3-268">Можно также использовать `@` символ для создания буквального строкового литерала, как было показано ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="978a3-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="978a3-269">Можно разбивать буквальные строковые литералы между строками:</span><span class="sxs-lookup"><span data-stu-id="978a3-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="978a3-270">Комментарии кода (и разметки)</span><span class="sxs-lookup"><span data-stu-id="978a3-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="978a3-271">Комментарии позволяют оставлять заметки для себя или для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="978a3-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="978a3-272">Они также позволяют отключить (*закомментировать*) раздел кода или разметки, которые не нужно запускать, но которые нужно оставить на странице в течение определенного времени.</span><span class="sxs-lookup"><span data-stu-id="978a3-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="978a3-273">Существует разный синтаксис комментариев для кода Razor и HTML-разметки.</span><span class="sxs-lookup"><span data-stu-id="978a3-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="978a3-274">Как и в случае с любым кодом Razor, комментарии Razor обрабатываются (а затем удаляются) на сервере перед отправкой страницы в браузер.</span><span class="sxs-lookup"><span data-stu-id="978a3-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="978a3-275">Поэтому синтаксис комментариев Razor позволяет добавлять комментарии в код (или даже в разметку), который можно увидеть при редактировании файла, но пользователи не видят даже в источнике страницы.</span><span class="sxs-lookup"><span data-stu-id="978a3-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="978a3-276">Для ASP.NET комментариев Razor необходимо начать комментарий с `@*` и завершить его `*@`.</span><span class="sxs-lookup"><span data-stu-id="978a3-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="978a3-277">Комментарий может находиться в одной строке или нескольких строках:</span><span class="sxs-lookup"><span data-stu-id="978a3-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="978a3-278">Вот комментарий в блоке кода:</span><span class="sxs-lookup"><span data-stu-id="978a3-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="978a3-279">Вот тот же блок кода, в котором строка кода была закомментироваться так, чтобы не выполнялась:</span><span class="sxs-lookup"><span data-stu-id="978a3-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="978a3-280">В блоке кода в качестве альтернативы синтаксису комментариев Razor можно использовать синтаксис комментариев языка программирования, который вы используете, например C#:</span><span class="sxs-lookup"><span data-stu-id="978a3-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="978a3-281">В C#однострочных комментариях предшествуют `//`ные символы, а многострочные комментарии начинаются с `/*` и заканчиваются `*/`.</span><span class="sxs-lookup"><span data-stu-id="978a3-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="978a3-282">(Как и в случае с C# комментариями Razor, комментарии не подготавливаются к просмотру в браузере.)</span><span class="sxs-lookup"><span data-stu-id="978a3-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="978a3-283">Для разметки, как вы, вероятно, знакомы, можно создать комментарий HTML:</span><span class="sxs-lookup"><span data-stu-id="978a3-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="978a3-284">Комментарии HTML начинаются с символов `<!--` и заканчиваются `-->`.</span><span class="sxs-lookup"><span data-stu-id="978a3-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="978a3-285">Можно использовать комментарии HTML, чтобы заключить не только текст, но и любую разметку HTML, которую можно оставить на странице, но не отображать.</span><span class="sxs-lookup"><span data-stu-id="978a3-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="978a3-286">Этот комментарий HTML скрывает все содержимое тегов и текст, который они содержат:</span><span class="sxs-lookup"><span data-stu-id="978a3-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="978a3-287">В отличие от комментариев *Razor комментарии HTML отображаются на* странице, а пользователь видит их, просматривая источник страницы.</span><span class="sxs-lookup"><span data-stu-id="978a3-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="978a3-288">Razor имеет ограничения на вложенные блоки C#.</span><span class="sxs-lookup"><span data-stu-id="978a3-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="978a3-289">Дополнительные сведения см. в разделе [ C# именованные переменные и вложенные блоки создание неработающего кода](http://aspnetwebstack.codeplex.com/workitem/1914)</span><span class="sxs-lookup"><span data-stu-id="978a3-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="978a3-290">Переменные</span><span class="sxs-lookup"><span data-stu-id="978a3-290">Variables</span></span>

<span data-ttu-id="978a3-291">Переменная — это именованный объект, который используется для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="978a3-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="978a3-292">Можно назвать любые переменные, но имя должно начинаться с буквы и не может содержать пробелы или зарезервированные символы.</span><span class="sxs-lookup"><span data-stu-id="978a3-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="978a3-293">Переменные и типы данных</span><span class="sxs-lookup"><span data-stu-id="978a3-293">Variables and Data Types</span></span>

<span data-ttu-id="978a3-294">Переменная может иметь конкретный тип данных, который указывает, какой тип данных хранится в переменной.</span><span class="sxs-lookup"><span data-stu-id="978a3-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="978a3-295">Можно использовать строковые переменные, которые хранят строковые значения (например, &quot;Hello World&quot;), целочисленные переменные, в которых хранятся целые значения (например, 3 или 79), и переменные даты, которые хранят значения дат в различных форматах (например, 4/12/2012 или Март 2009).</span><span class="sxs-lookup"><span data-stu-id="978a3-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="978a3-296">И существует много других типов данных, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="978a3-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="978a3-297">Однако обычно для переменной не нужно указывать тип.</span><span class="sxs-lookup"><span data-stu-id="978a3-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="978a3-298">В большинстве случаев ASP.NET может определить тип в зависимости от того, как используются данные в переменной.</span><span class="sxs-lookup"><span data-stu-id="978a3-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="978a3-299">(Иногда необходимо указать тип; вы увидите примеры, в которых это верно.)</span><span class="sxs-lookup"><span data-stu-id="978a3-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="978a3-300">Переменная объявляется с помощью ключевого слова `var` (если вы не хотите указывать тип) или с помощью имени типа:</span><span class="sxs-lookup"><span data-stu-id="978a3-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="978a3-301">В следующем примере показаны некоторые типичные способы использования переменных на веб-странице:</span><span class="sxs-lookup"><span data-stu-id="978a3-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="978a3-302">Если вы объединяете предыдущие примеры на странице, вы увидите, что они отображаются в браузере:</span><span class="sxs-lookup"><span data-stu-id="978a3-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor — Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="978a3-304">Преобразование и тестирование типов данных</span><span class="sxs-lookup"><span data-stu-id="978a3-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="978a3-305">Хотя ASP.NET обычно может определять тип данных автоматически, иногда он не может.</span><span class="sxs-lookup"><span data-stu-id="978a3-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="978a3-306">Таким образом, может потребоваться помочь ASP.NET, выполнив явное преобразование.</span><span class="sxs-lookup"><span data-stu-id="978a3-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="978a3-307">Даже если нет необходимости в преобразовании типов, иногда полезно проверить, какие типы данных могут быть вам доступны.</span><span class="sxs-lookup"><span data-stu-id="978a3-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="978a3-308">Наиболее распространенным случаем является преобразование строки в другой тип, например в Integer или Date.</span><span class="sxs-lookup"><span data-stu-id="978a3-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="978a3-309">В следующем примере показан типичный случай, когда необходимо преобразовать строку в число.</span><span class="sxs-lookup"><span data-stu-id="978a3-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="978a3-310">Как правило, вводимые пользователем данные поступают в виде строк.</span><span class="sxs-lookup"><span data-stu-id="978a3-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="978a3-311">Даже если вы предоставили пользователю запрос на ввод числа, и даже если они вводили цифру, при отправке введенных пользователем данных и считывании их в коде данные представлены в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="978a3-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="978a3-312">Поэтому необходимо преобразовать строку в число.</span><span class="sxs-lookup"><span data-stu-id="978a3-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="978a3-313">В этом примере, если вы попытаетесь выполнить арифметические действия со значениями без их преобразования, выдается следующее сообщение об ошибке, так как ASP.NET не может добавить две строки:</span><span class="sxs-lookup"><span data-stu-id="978a3-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="978a3-314">*Невозможно неявно преобразовать тип "String" в "int".*</span><span class="sxs-lookup"><span data-stu-id="978a3-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="978a3-315">Чтобы преобразовать значения в целые числа, вызовите метод `AsInt`.</span><span class="sxs-lookup"><span data-stu-id="978a3-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="978a3-316">Если преобразование выполнено успешно, можно добавить числа.</span><span class="sxs-lookup"><span data-stu-id="978a3-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="978a3-317">В следующей таблице перечислены некоторые распространенные методы преобразования и тестирования для переменных.</span><span class="sxs-lookup"><span data-stu-id="978a3-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="978a3-318"><strong>Метод</strong></span><span class="sxs-lookup"><span data-stu-id="978a3-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-319"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="978a3-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-320"><strong>Пример</strong></span><span class="sxs-lookup"><span data-stu-id="978a3-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-321">Преобразует строку, представляющую целое число (например, "593"), в целочисленное значение.</span><span class="sxs-lookup"><span data-stu-id="978a3-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-322">Преобразует строку, такую как &quot;true&quot; или &quot;false&quot;, в логический тип.</span><span class="sxs-lookup"><span data-stu-id="978a3-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-323">Преобразует строку, имеющую десятичное значение, например &quot;1,3&quot; или &quot;7,439&quot;, в число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="978a3-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-324">Преобразует строку, имеющую десятичное значение, например &quot;1,3&quot; или &quot;7,439&quot;, в десятичное число.</span><span class="sxs-lookup"><span data-stu-id="978a3-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="978a3-325">(В ASP.NET десятичное число является более точным, чем число с плавающей запятой.)</span><span class="sxs-lookup"><span data-stu-id="978a3-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-326">Преобразует строку, представляющую значение даты и времени, в тип `DateTime` ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="978a3-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-327">Преобразует любой другой тип данных в строку.</span><span class="sxs-lookup"><span data-stu-id="978a3-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="978a3-328">Операторы</span><span class="sxs-lookup"><span data-stu-id="978a3-328">Operators</span></span>

<span data-ttu-id="978a3-329">Оператор — это ключевое слово или символ, который сообщает ASP.NET, какой тип команды выполнять в выражении.</span><span class="sxs-lookup"><span data-stu-id="978a3-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="978a3-330">C# Язык (и синтаксис Razor, основанный на нем) поддерживает множество операторов, но для начала работы нужно только определить несколько.</span><span class="sxs-lookup"><span data-stu-id="978a3-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="978a3-331">В следующей таблице перечислены наиболее распространенные операторы.</span><span class="sxs-lookup"><span data-stu-id="978a3-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="978a3-332"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="978a3-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-333"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="978a3-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-334"><strong>Примеры</strong></span><span class="sxs-lookup"><span data-stu-id="978a3-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="978a3-335">`+` `-` `*` `/`</span><span class="sxs-lookup"><span data-stu-id="978a3-335">`+` `-` `*` `/`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-336">Математические операторы, используемые в числовых выражениях.</span><span class="sxs-lookup"><span data-stu-id="978a3-336">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-337">Присваивание.</span><span class="sxs-lookup"><span data-stu-id="978a3-337">Assignment.</span></span> <span data-ttu-id="978a3-338">Присваивает значение в правой части оператора объекту с левой стороны.</span><span class="sxs-lookup"><span data-stu-id="978a3-338">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-339">Равенство.</span><span class="sxs-lookup"><span data-stu-id="978a3-339">Equality.</span></span> <span data-ttu-id="978a3-340">Возвращает `true`, если значения равны.</span><span class="sxs-lookup"><span data-stu-id="978a3-340">Returns `true` if the values are equal.</span></span> <span data-ttu-id="978a3-341">(Обратите внимание на различие между оператором `=` и оператором `==`.)</span><span class="sxs-lookup"><span data-stu-id="978a3-341">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-342">Неравенство.</span><span class="sxs-lookup"><span data-stu-id="978a3-342">Inequality.</span></span> <span data-ttu-id="978a3-343">Возвращает `true`, если значения не равны.</span><span class="sxs-lookup"><span data-stu-id="978a3-343">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-344">"Меньше", "больше чем", "меньше или равно" и "больше или равно".</span><span class="sxs-lookup"><span data-stu-id="978a3-344">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-345">Объединение, которое используется для соединения строк.</span><span class="sxs-lookup"><span data-stu-id="978a3-345">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="978a3-346">ASP.NET знает разницу между этим оператором и оператором сложения в зависимости от типа данных выражения.</span><span class="sxs-lookup"><span data-stu-id="978a3-346">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="978a3-347">`+=` `-=`</span><span class="sxs-lookup"><span data-stu-id="978a3-347">`+=` `-=`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-348">Операторы инкремента и декремента, которые добавляют и вычитают 1 (соответственно) из переменной.</span><span class="sxs-lookup"><span data-stu-id="978a3-348">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-349">Оператор.</span><span class="sxs-lookup"><span data-stu-id="978a3-349">Dot.</span></span> <span data-ttu-id="978a3-350">Используется для различения объектов и их свойств и методов.</span><span class="sxs-lookup"><span data-stu-id="978a3-350">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-351">Скобки.</span><span class="sxs-lookup"><span data-stu-id="978a3-351">Parentheses.</span></span> <span data-ttu-id="978a3-352">Используется для группирования выражений и передачи параметров методам.</span><span class="sxs-lookup"><span data-stu-id="978a3-352">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-353">Квадратных.</span><span class="sxs-lookup"><span data-stu-id="978a3-353">Brackets.</span></span> <span data-ttu-id="978a3-354">Используется для доступа к значениям в массивах или коллекциях.</span><span class="sxs-lookup"><span data-stu-id="978a3-354">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-355">Недостаточно.</span><span class="sxs-lookup"><span data-stu-id="978a3-355">Not.</span></span> <span data-ttu-id="978a3-356">Изменяет значение `true` на `false` и наоборот.</span><span class="sxs-lookup"><span data-stu-id="978a3-356">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="978a3-357">Обычно используется в качестве краткого способа проверки `false` (то есть не `true`).</span><span class="sxs-lookup"><span data-stu-id="978a3-357">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="978a3-358">`&&` `||`</span><span class="sxs-lookup"><span data-stu-id="978a3-358">`&&` `||`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="978a3-359">Логические и и OR, которые используются для связи условий.</span><span class="sxs-lookup"><span data-stu-id="978a3-359">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="978a3-360">Работа с путями к файлам и папкам в коде</span><span class="sxs-lookup"><span data-stu-id="978a3-360">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="978a3-361">Вы часто работаете с путями к файлам и папкам в коде.</span><span class="sxs-lookup"><span data-stu-id="978a3-361">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="978a3-362">Ниже приведен пример структуры физической папки для веб-сайта, который может отображаться на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="978a3-362">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="978a3-363">Ниже приведены некоторые основные сведения о URL-адресах и путях.</span><span class="sxs-lookup"><span data-stu-id="978a3-363">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="978a3-364">URL-адрес начинается с доменного имени (`http://www.example.com`) или имени сервера (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="978a3-364">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="978a3-365">URL-адрес соответствует физическому пути на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="978a3-365">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="978a3-366">Например, `http://myserver` может соответствовать папке *к:\вебситес\мивебсите* на сервере.</span><span class="sxs-lookup"><span data-stu-id="978a3-366">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="978a3-367">Виртуальный путь является краткой для представления путей в коде без указания полного пути.</span><span class="sxs-lookup"><span data-stu-id="978a3-367">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="978a3-368">Он включает часть URL-адреса, следующую за именем домена или сервера.</span><span class="sxs-lookup"><span data-stu-id="978a3-368">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="978a3-369">При использовании виртуальных путей можно переместить код в другой домен или сервер без необходимости обновлять пути.</span><span class="sxs-lookup"><span data-stu-id="978a3-369">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="978a3-370">Ниже приведен пример, который поможет понять различия:</span><span class="sxs-lookup"><span data-stu-id="978a3-370">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="978a3-371">Полный URL-адрес</span><span class="sxs-lookup"><span data-stu-id="978a3-371">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="978a3-372">Имя сервера</span><span class="sxs-lookup"><span data-stu-id="978a3-372">Server name</span></span> | <span data-ttu-id="978a3-373">*микомпанисервер*</span><span class="sxs-lookup"><span data-stu-id="978a3-373">*mycompanyserver*</span></span> |
| <span data-ttu-id="978a3-374">Виртуальный путь</span><span class="sxs-lookup"><span data-stu-id="978a3-374">Virtual path</span></span> | <span data-ttu-id="978a3-375">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="978a3-375">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="978a3-376">Физический путь</span><span class="sxs-lookup"><span data-stu-id="978a3-376">Physical path</span></span> | <span data-ttu-id="978a3-377">*к:\мивебситес\хуманресаурцес\компаниполици.хтм*</span><span class="sxs-lookup"><span data-stu-id="978a3-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="978a3-378">Виртуальный корень имеет значение/, как и корневой каталог диска C: \.</span><span class="sxs-lookup"><span data-stu-id="978a3-378">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="978a3-379">(Пути к виртуальным папкам всегда используют косую черту.) Виртуальный путь к папке не должен совпадать с именем физической папки. Это может быть псевдоним.</span><span class="sxs-lookup"><span data-stu-id="978a3-379">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="978a3-380">(На рабочих серверах виртуальный путь редко соответствует точному физическому пути.)</span><span class="sxs-lookup"><span data-stu-id="978a3-380">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="978a3-381">При работе с файлами и папками в коде иногда требуется ссылка на физический путь и иногда виртуальный путь в зависимости от объектов, с которыми вы работаете.</span><span class="sxs-lookup"><span data-stu-id="978a3-381">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="978a3-382">ASP.NET предоставляет следующие средства для работы с путями к файлам и папкам в коде: метод `Server.MapPath`, оператор `~` и метод `Href`.</span><span class="sxs-lookup"><span data-stu-id="978a3-382">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="978a3-383">Преобразование виртуальных в физические пути: метод Server. MapPath</span><span class="sxs-lookup"><span data-stu-id="978a3-383">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="978a3-384">Метод `Server.MapPath` Преобразует виртуальный путь (например, */дефаулт.кштмл*) в абсолютный физический путь (например, *к:\вебситес\мивебситефолдер\дефаулт.кштмл*).</span><span class="sxs-lookup"><span data-stu-id="978a3-384">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="978a3-385">Этот метод используется в любой момент, когда требуется полный физический путь.</span><span class="sxs-lookup"><span data-stu-id="978a3-385">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="978a3-386">Типичный пример — при чтении или записи текстового файла или файла изображения на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="978a3-386">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="978a3-387">Как правило, абсолютный физический путь к сайту на сервере узла размещения не известен, поэтому этот метод может преобразовать известный путь (виртуальный путь) в соответствующий путь на сервере.</span><span class="sxs-lookup"><span data-stu-id="978a3-387">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="978a3-388">Виртуальный путь передается в файл или папку в метод и возвращает физический путь:</span><span class="sxs-lookup"><span data-stu-id="978a3-388">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="978a3-389">Ссылка на виртуальный корень: оператор ~ и метод href</span><span class="sxs-lookup"><span data-stu-id="978a3-389">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="978a3-390">В файле *. cshtml* или *. vbhtml* можно ссылаться на виртуальный корневой путь с помощью оператора `~`.</span><span class="sxs-lookup"><span data-stu-id="978a3-390">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="978a3-391">Это очень удобно, так как можно перемещать страницы на сайте и любые ссылки, содержащиеся на других страницах, не будут разорваны.</span><span class="sxs-lookup"><span data-stu-id="978a3-391">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="978a3-392">Это также удобно, если вы перемещаете веб-сайт в другое место.</span><span class="sxs-lookup"><span data-stu-id="978a3-392">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="978a3-393">Далее приводятся некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="978a3-393">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="978a3-394">Если веб-сайт `http://myserver/myapp`, то, как ASP.NET будет обрабатывать эти пути при выполнении страницы:</span><span class="sxs-lookup"><span data-stu-id="978a3-394">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="978a3-395">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="978a3-395">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="978a3-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="978a3-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="978a3-397">(В действительности эти пути не отображаются как значения переменной, но ASP.NET будет рассматривать пути так, как будто они были.)</span><span class="sxs-lookup"><span data-stu-id="978a3-397">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="978a3-398">Оператор `~` можно использовать как в коде сервера (как описано выше), так и в разметке следующим образом:</span><span class="sxs-lookup"><span data-stu-id="978a3-398">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="978a3-399">В разметке оператор `~` используется для создания путей к ресурсам, таким как файлы изображений, другие веб-страницы и файлы CSS.</span><span class="sxs-lookup"><span data-stu-id="978a3-399">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="978a3-400">При запуске страницы ASP.NET просматривает страницу (как код, так и разметку) и разрешает все `~` ссылки на соответствующий путь.</span><span class="sxs-lookup"><span data-stu-id="978a3-400">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="978a3-401">Условная логика и циклы</span><span class="sxs-lookup"><span data-stu-id="978a3-401">Conditional Logic and Loops</span></span>

<span data-ttu-id="978a3-402">ASP.NET Server Code позволяет выполнять задачи на основе условий и писать код, который повторяет инструкции определенное число раз (то есть код, выполняющий цикл).</span><span class="sxs-lookup"><span data-stu-id="978a3-402">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="978a3-403">Условия тестирования</span><span class="sxs-lookup"><span data-stu-id="978a3-403">Testing Conditions</span></span>

<span data-ttu-id="978a3-404">Чтобы проверить простое условие, используйте инструкцию `if`, которая возвращает значение true или false в зависимости от указанного теста:</span><span class="sxs-lookup"><span data-stu-id="978a3-404">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="978a3-405">Ключевое слово `if` запускает блок.</span><span class="sxs-lookup"><span data-stu-id="978a3-405">The `if` keyword starts a block.</span></span> <span data-ttu-id="978a3-406">Фактический тест (условие) задается в круглых скобках и возвращает значение true или false.</span><span class="sxs-lookup"><span data-stu-id="978a3-406">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="978a3-407">Инструкции, выполняемые, если тест имеет значение true, заключены в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="978a3-407">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="978a3-408">Инструкция `if` может включать блок `else`, указывающий, какие операторы выполняются, если условие ложно:</span><span class="sxs-lookup"><span data-stu-id="978a3-408">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="978a3-409">Можно добавить несколько условий с помощью блока `else if`.</span><span class="sxs-lookup"><span data-stu-id="978a3-409">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="978a3-410">В этом примере, если первое условие в блоке if не равно true, проверяется условие `else if`.</span><span class="sxs-lookup"><span data-stu-id="978a3-410">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="978a3-411">Если это условие выполнено, выполняются инструкции в блоке `else if`.</span><span class="sxs-lookup"><span data-stu-id="978a3-411">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="978a3-412">Если ни одно из условий не соблюдается, выполняются инструкции в блоке `else`.</span><span class="sxs-lookup"><span data-stu-id="978a3-412">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="978a3-413">Можно добавить любое количество else if, а затем закрыть блок `else` как &quot;все остальное&quot; условие.</span><span class="sxs-lookup"><span data-stu-id="978a3-413">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="978a3-414">Чтобы проверить большое количество условий, используйте блок `switch`:</span><span class="sxs-lookup"><span data-stu-id="978a3-414">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="978a3-415">Проверяемое значение находится в круглых скобках (в примере это переменная `weekday`).</span><span class="sxs-lookup"><span data-stu-id="978a3-415">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="978a3-416">Каждый отдельный тест использует инструкцию `case`, которая заканчивается двоеточием (:).</span><span class="sxs-lookup"><span data-stu-id="978a3-416">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="978a3-417">Если значение инструкции `case` соответствует тестовому значению, выполняется код в этом блоке Case.</span><span class="sxs-lookup"><span data-stu-id="978a3-417">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="978a3-418">Каждый оператор Case закрывается с помощью оператора `break`.</span><span class="sxs-lookup"><span data-stu-id="978a3-418">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="978a3-419">(Если вы забыли включить break в каждом блоке `case`, будет также выполняться код из следующей `case`.) Блок `switch` часто содержит оператор `default`, как в последнем случае &quot;все остальное&quot;, которое выполняется, если ни одно из других случаев не выполняется.</span><span class="sxs-lookup"><span data-stu-id="978a3-419">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="978a3-420">Результат двух последних условных блоков, отображаемых в браузере:</span><span class="sxs-lookup"><span data-stu-id="978a3-420">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor — Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="978a3-422">Циклическое выполнение кода</span><span class="sxs-lookup"><span data-stu-id="978a3-422">Looping Code</span></span>

<span data-ttu-id="978a3-423">Часто приходится многократно выполнять одни и те же инструкции.</span><span class="sxs-lookup"><span data-stu-id="978a3-423">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="978a3-424">Для этого нужно выполнить цикл.</span><span class="sxs-lookup"><span data-stu-id="978a3-424">You do this by looping.</span></span> <span data-ttu-id="978a3-425">Например, часто выполняются одни и те же инструкции для каждого элемента в коллекции данных.</span><span class="sxs-lookup"><span data-stu-id="978a3-425">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="978a3-426">Если точно известно, сколько раз вы хотите пройти цикл, можно использовать цикл `for`.</span><span class="sxs-lookup"><span data-stu-id="978a3-426">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="978a3-427">Этот тип цикла особенно полезен для подсчета или пересчета:</span><span class="sxs-lookup"><span data-stu-id="978a3-427">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="978a3-428">Цикл начинается с ключевого слова `for`, за которым следуют три оператора в круглых скобках, каждый из которых завершается точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="978a3-428">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="978a3-429">В круглых скобках первый оператор (`var i=10;`) создает счетчик и инициализирует его до 10.</span><span class="sxs-lookup"><span data-stu-id="978a3-429">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="978a3-430">Вам не нужно присвоить значение счетчику, `i` &#8212; можно использовать любую переменную.</span><span class="sxs-lookup"><span data-stu-id="978a3-430">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="978a3-431">При выполнении цикла `for` автоматически увеличивается значение счетчика.</span><span class="sxs-lookup"><span data-stu-id="978a3-431">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="978a3-432">Вторая инструкция (`i < 21;`) задает условие того, насколько вы хотите подсчитать.</span><span class="sxs-lookup"><span data-stu-id="978a3-432">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="978a3-433">В этом случае вы хотите, чтобы он не превышал значение 20 (то есть, пока значение счетчика меньше 21).</span><span class="sxs-lookup"><span data-stu-id="978a3-433">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="978a3-434">Третья инструкция (`i++`) использует оператор инкремента, который просто указывает, что счетчик должен иметь 1 к нему каждый раз при выполнении цикла.</span><span class="sxs-lookup"><span data-stu-id="978a3-434">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="978a3-435">Внутри фигурных скобок находится код, который будет выполняться для каждой итерации цикла.</span><span class="sxs-lookup"><span data-stu-id="978a3-435">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="978a3-436">Разметка создает новый абзац (`<p>` элемент) каждый раз и добавляет строку к выходу, отображая значение `i` (счетчик).</span><span class="sxs-lookup"><span data-stu-id="978a3-436">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="978a3-437">При запуске этой страницы в примере создаются 11 строк, в которых отображаются выходные данные, и текст в каждой строке, указывающей на номер товара.</span><span class="sxs-lookup"><span data-stu-id="978a3-437">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor — Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="978a3-439">При работе с коллекцией или массивом часто используется цикл `foreach`.</span><span class="sxs-lookup"><span data-stu-id="978a3-439">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="978a3-440">Коллекция — это группа схожих объектов, а цикл `foreach` позволяет выполнять задачу для каждого элемента в коллекции.</span><span class="sxs-lookup"><span data-stu-id="978a3-440">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="978a3-441">Этот тип цикла удобен для коллекций, так как в отличие от цикла `for` не нужно увеличивать счетчик или устанавливать ограничение.</span><span class="sxs-lookup"><span data-stu-id="978a3-441">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="978a3-442">Вместо этого код цикла `foreach` просто проходит по коллекции, пока не завершится.</span><span class="sxs-lookup"><span data-stu-id="978a3-442">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="978a3-443">Например, следующий код возвращает элементы коллекции `Request.ServerVariables`, которая представляет собой объект, содержащий сведения о веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="978a3-443">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="978a3-444">В нем используется цикл `foreac` h для вывода имени каждого элемента путем создания нового элемента `<li>` в маркированном списке HTML.</span><span class="sxs-lookup"><span data-stu-id="978a3-444">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="978a3-445">За ключевым словом `foreach` следуют круглые скобки, в которых объявляется переменная, представляющая один элемент в коллекции (в примере — `var item`), за которой следует ключевое слово `in`, а затем Коллекция, которую необходимо прокручивать.</span><span class="sxs-lookup"><span data-stu-id="978a3-445">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="978a3-446">В теле цикла `foreach` можно получить доступ к текущему элементу с помощью объявленной ранее переменной.</span><span class="sxs-lookup"><span data-stu-id="978a3-446">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor — Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="978a3-448">Чтобы создать более общий цикл общего назначения, используйте оператор `while`:</span><span class="sxs-lookup"><span data-stu-id="978a3-448">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="978a3-449">Цикл `while` начинается с ключевого слова `while`, за которым следуют круглые скобки, в которых указывается, как долго будет продолжаться цикл (в случае, если `countNum` меньше 50), а затем для повторения блока.</span><span class="sxs-lookup"><span data-stu-id="978a3-449">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="978a3-450">Циклы обычно увеличивают (добавляются в) или уменьшают (вычитаются из) переменную или объект, используемый для подсчета.</span><span class="sxs-lookup"><span data-stu-id="978a3-450">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="978a3-451">В этом примере оператор `+=` добавляет 1 к `countNum` при каждом запуске цикла.</span><span class="sxs-lookup"><span data-stu-id="978a3-451">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="978a3-452">(Чтобы уменьшить переменную в цикле, который подсчитывается вниз, используйте оператор декремента `-=`).</span><span class="sxs-lookup"><span data-stu-id="978a3-452">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="978a3-453">Объекты и коллекции</span><span class="sxs-lookup"><span data-stu-id="978a3-453">Objects and Collections</span></span>

<span data-ttu-id="978a3-454">Практически все на веб-сайте ASP.NET — это объект, включая саму веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="978a3-454">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="978a3-455">В этом разделе обсуждаются некоторые важные объекты, с которыми часто приходится работать в коде.</span><span class="sxs-lookup"><span data-stu-id="978a3-455">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="978a3-456">Объекты Page</span><span class="sxs-lookup"><span data-stu-id="978a3-456">Page Objects</span></span>

<span data-ttu-id="978a3-457">Самым основным объектом в ASP.NET является страница.</span><span class="sxs-lookup"><span data-stu-id="978a3-457">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="978a3-458">Вы можете обращаться к свойствам объекта Page напрямую, не используя соответствующий объект.</span><span class="sxs-lookup"><span data-stu-id="978a3-458">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="978a3-459">Следующий код получает путь к файлу страницы, используя объект `Request` страницы:</span><span class="sxs-lookup"><span data-stu-id="978a3-459">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="978a3-460">Чтобы ясно, что вы ссылаетесь на свойства и методы объекта текущей страницы, при необходимости можно использовать ключевое слово `this` для представления объекта страницы в коде.</span><span class="sxs-lookup"><span data-stu-id="978a3-460">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="978a3-461">Ниже приведен предыдущий пример кода с `this` добавленным для представления страницы:</span><span class="sxs-lookup"><span data-stu-id="978a3-461">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="978a3-462">Вы можете использовать свойства объекта `Page` для получения большого объема информации, например:</span><span class="sxs-lookup"><span data-stu-id="978a3-462">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="978a3-463">`Request`.</span><span class="sxs-lookup"><span data-stu-id="978a3-463">`Request`.</span></span> <span data-ttu-id="978a3-464">Как уже было показано, это коллекция сведений о текущем запросе, включая тип браузера, который сделал запрос, URL-адрес страницы, удостоверение пользователя и т. д.</span><span class="sxs-lookup"><span data-stu-id="978a3-464">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="978a3-465">`Response`.</span><span class="sxs-lookup"><span data-stu-id="978a3-465">`Response`.</span></span> <span data-ttu-id="978a3-466">Это коллекция сведений о ответе (странице), которая будет отправлена в браузер после завершения выполнения кода сервера.</span><span class="sxs-lookup"><span data-stu-id="978a3-466">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="978a3-467">Например, это свойство можно использовать для записи сведений в ответ.</span><span class="sxs-lookup"><span data-stu-id="978a3-467">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="978a3-468">Объекты коллекции (массивы и словари)</span><span class="sxs-lookup"><span data-stu-id="978a3-468">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="978a3-469">*Коллекция* — это группа объектов одного типа, например коллекция объектов `Customer` из базы данных.</span><span class="sxs-lookup"><span data-stu-id="978a3-469">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="978a3-470">ASP.NET содержит множество встроенных коллекций, таких как коллекция `Request.Files`.</span><span class="sxs-lookup"><span data-stu-id="978a3-470">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="978a3-471">Вы часто работаете с данными в коллекциях.</span><span class="sxs-lookup"><span data-stu-id="978a3-471">You'll often work with data in collections.</span></span> <span data-ttu-id="978a3-472">Два общих типа коллекций — это *массив* и *словарь*.</span><span class="sxs-lookup"><span data-stu-id="978a3-472">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="978a3-473">Массив полезен, если нужно сохранить коллекцию схожих элементов, но не нужно создавать отдельную переменную для хранения каждого элемента:</span><span class="sxs-lookup"><span data-stu-id="978a3-473">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="978a3-474">При использовании массивов вы объявляете конкретный тип данных, например `string`, `int`или `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="978a3-474">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="978a3-475">Чтобы указать, что переменная может содержать массив, добавьте в объявление скобки (например, `string[]` или `int[]`).</span><span class="sxs-lookup"><span data-stu-id="978a3-475">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="978a3-476">Доступ к элементам массива можно получить с помощью их позиции (индекса) или с помощью инструкции `foreach`.</span><span class="sxs-lookup"><span data-stu-id="978a3-476">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="978a3-477">Индексы массива отсчитываются от &#8212; нуля, т. е. первый элемент находится в позиции 0, второй элемент — в позиции 1 и т. д.</span><span class="sxs-lookup"><span data-stu-id="978a3-477">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="978a3-478">Чтобы определить количество элементов в массиве, можно получить свойство `Length`.</span><span class="sxs-lookup"><span data-stu-id="978a3-478">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="978a3-479">Чтобы получить позицию определенного элемента в массиве (для поиска в массиве), используйте метод `Array.IndexOf`.</span><span class="sxs-lookup"><span data-stu-id="978a3-479">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="978a3-480">Можно также выполнять такие действия, как обратный порядок содержимого массива (метод `Array.Reverse`) или сортировать содержимое (метод `Array.Sort`).</span><span class="sxs-lookup"><span data-stu-id="978a3-480">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="978a3-481">Выходные данные кода массива строк, отображаемого в браузере:</span><span class="sxs-lookup"><span data-stu-id="978a3-481">The output of the string array code displayed in a browser:</span></span>

![Razor — Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="978a3-483">Словарь — это коллекция пар "ключ-значение", где вы предоставляете ключ (или имя) для установки или получения соответствующего значения:</span><span class="sxs-lookup"><span data-stu-id="978a3-483">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="978a3-484">Чтобы создать словарь, используйте ключевое слово `new`, чтобы указать, что вы создаете новый объект Dictionary.</span><span class="sxs-lookup"><span data-stu-id="978a3-484">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="978a3-485">Можно назначить словарь переменной с помощью ключевого слова `var`.</span><span class="sxs-lookup"><span data-stu-id="978a3-485">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="978a3-486">Типы данных элементов в словаре указываются с помощью угловых скобок (`< >`).</span><span class="sxs-lookup"><span data-stu-id="978a3-486">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="978a3-487">В конце объявления необходимо добавить пару круглых скобок, поскольку это фактически метод, создающий новый словарь.</span><span class="sxs-lookup"><span data-stu-id="978a3-487">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="978a3-488">Чтобы добавить элементы в словарь, можно вызвать метод `Add` переменной Dictionary (`myScores` в этом случае), а затем указать ключ и значение.</span><span class="sxs-lookup"><span data-stu-id="978a3-488">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="978a3-489">Кроме того, можно использовать квадратные скобки для обозначения ключа и выполнить простое назначение, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="978a3-489">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="978a3-490">Чтобы получить значение из словаря, необходимо указать ключ в квадратных скобках:</span><span class="sxs-lookup"><span data-stu-id="978a3-490">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="978a3-491">Вызов методов с параметрами</span><span class="sxs-lookup"><span data-stu-id="978a3-491">Calling Methods with Parameters</span></span>

<span data-ttu-id="978a3-492">По мере прочтения в этой статье объекты, с которыми Вы запрограммированы, могут иметь методы.</span><span class="sxs-lookup"><span data-stu-id="978a3-492">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="978a3-493">Например, объект `Database` может иметь метод `Database.Connect`.</span><span class="sxs-lookup"><span data-stu-id="978a3-493">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="978a3-494">Многие методы также имеют один или несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="978a3-494">Many methods also have one or more parameters.</span></span> <span data-ttu-id="978a3-495">*Параметр* — это значение, передаваемое в метод, чтобы позволить методу завершить свою задачу.</span><span class="sxs-lookup"><span data-stu-id="978a3-495">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="978a3-496">Например, рассмотрим объявление метода `Request.MapPath`, который принимает три параметра:</span><span class="sxs-lookup"><span data-stu-id="978a3-496">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="978a3-497">(Строка была заключена в оболочку, чтобы сделать ее более удобочитаемой.</span><span class="sxs-lookup"><span data-stu-id="978a3-497">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="978a3-498">Помните, что разрывы строк можно поместить почти в любое место, за исключением строк, заключенных в кавычки.)</span><span class="sxs-lookup"><span data-stu-id="978a3-498">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="978a3-499">Этот метод возвращает физический путь на сервере, соответствующий указанному виртуальному пути.</span><span class="sxs-lookup"><span data-stu-id="978a3-499">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="978a3-500">Три параметра для метода: `virtualPath`, `baseVirtualDir`и `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="978a3-500">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="978a3-501">(Обратите внимание, что в объявлении указаны параметры с типами данных, которые они будут принимать.) При вызове этого метода необходимо указать значения для всех трех параметров.</span><span class="sxs-lookup"><span data-stu-id="978a3-501">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="978a3-502">Синтаксис Razor предоставляет два варианта передачи параметров в метод: *позиционированные параметры* и *именованные параметры*.</span><span class="sxs-lookup"><span data-stu-id="978a3-502">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="978a3-503">Чтобы вызвать метод с помощью методов с параметрами, необходимо передать параметры в определенном порядке, указанном в объявлении метода.</span><span class="sxs-lookup"><span data-stu-id="978a3-503">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="978a3-504">(Обычно этот порядок вы узнаете, читая документацию по методу.) Необходимо соблюдать порядок следования, и при необходимости нельзя пропустить какие-либо &#8212; параметры, передавая пустую строку (`""`) или `null` для параметра, для которого у вас нет значения.</span><span class="sxs-lookup"><span data-stu-id="978a3-504">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="978a3-505">В следующем примере предполагается, что на веб-сайте есть папка с именем *Scripts* .</span><span class="sxs-lookup"><span data-stu-id="978a3-505">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="978a3-506">Код вызывает метод `Request.MapPath` и передает значения для трех параметров в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="978a3-506">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="978a3-507">Затем отображается полученный сопоставленный путь.</span><span class="sxs-lookup"><span data-stu-id="978a3-507">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="978a3-508">Если у метода много параметров, можно сделать код более читаемым, используя именованные параметры.</span><span class="sxs-lookup"><span data-stu-id="978a3-508">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="978a3-509">Чтобы вызвать метод с использованием именованных параметров, укажите имя параметра, за которым следует двоеточие (:), а затем значение.</span><span class="sxs-lookup"><span data-stu-id="978a3-509">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="978a3-510">Преимущество именованных параметров заключается в том, что их можно передавать в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="978a3-510">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="978a3-511">(Недостаток заключается в том, что вызов метода не является компактным.)</span><span class="sxs-lookup"><span data-stu-id="978a3-511">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="978a3-512">В следующем примере вызывается тот же метод, что и выше, но для предоставления значений используются именованные параметры:</span><span class="sxs-lookup"><span data-stu-id="978a3-512">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="978a3-513">Как видите, параметры передаются в другом порядке.</span><span class="sxs-lookup"><span data-stu-id="978a3-513">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="978a3-514">Однако если запустить предыдущий пример и этот пример, они будут возвращать одно и то же значение.</span><span class="sxs-lookup"><span data-stu-id="978a3-514">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="978a3-515">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="978a3-515">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="978a3-516">Операторы Try-Catch</span><span class="sxs-lookup"><span data-stu-id="978a3-516">Try-Catch Statements</span></span>

<span data-ttu-id="978a3-517">Часто в коде есть операторы, которые могут завершиться ошибкой по причинам, находящимся за пределами элемента управления.</span><span class="sxs-lookup"><span data-stu-id="978a3-517">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="978a3-518">Например:</span><span class="sxs-lookup"><span data-stu-id="978a3-518">For example:</span></span>

- <span data-ttu-id="978a3-519">Если код пытается создать файл или получить к нему доступ, могут возникать все виды ошибок.</span><span class="sxs-lookup"><span data-stu-id="978a3-519">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="978a3-520">Возможно, нужный файл не существует, он может быть заблокирован, код может не иметь разрешений и т. д.</span><span class="sxs-lookup"><span data-stu-id="978a3-520">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="978a3-521">Аналогично, если код пытается обновить записи в базе данных, могут возникнуть проблемы с разрешениями, подключение к базе данных может быть удалено, данные для сохранения могут быть недействительными и т. д.</span><span class="sxs-lookup"><span data-stu-id="978a3-521">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="978a3-522">В терминах программирования эти ситуации называются *исключениями*.</span><span class="sxs-lookup"><span data-stu-id="978a3-522">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="978a3-523">Если код сталкивается с исключением, он создает (выдает) сообщение об ошибке, которое лучше подойдет для пользователей:</span><span class="sxs-lookup"><span data-stu-id="978a3-523">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor — Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="978a3-525">В ситуациях, когда код может столкнуться с исключениями и во избежание сообщений об ошибках этого типа, можно использовать инструкции `try/catch`.</span><span class="sxs-lookup"><span data-stu-id="978a3-525">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="978a3-526">В инструкции `try` выполняется проверка кода.</span><span class="sxs-lookup"><span data-stu-id="978a3-526">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="978a3-527">В одной или нескольких инструкциях `catch` можно найти определенные ошибки (определенные типы исключений), которые могли произойти.</span><span class="sxs-lookup"><span data-stu-id="978a3-527">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="978a3-528">Можно включить столько `catch` инструкций, сколько необходимо для поиска ожидаемых ошибок.</span><span class="sxs-lookup"><span data-stu-id="978a3-528">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="978a3-529">Рекомендуется избегать использования метода `Response.Redirect` в инструкциях `try/catch`, так как это может вызвать исключение на странице.</span><span class="sxs-lookup"><span data-stu-id="978a3-529">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="978a3-530">В следующем примере показана страница, которая создает текстовый файл при первом запросе, а затем отображает кнопку, которая позволяет пользователю открыть файл.</span><span class="sxs-lookup"><span data-stu-id="978a3-530">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="978a3-531">В этом примере преднамеренно используется неправильное имя файла, что вызовет исключение.</span><span class="sxs-lookup"><span data-stu-id="978a3-531">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="978a3-532">Код включает `catch` операторы для двух возможных исключений: `FileNotFoundException`, которое происходит, если имя файла является недопустимым, и `DirectoryNotFoundException`, что происходит, если ASP.NET даже не может найти папку.</span><span class="sxs-lookup"><span data-stu-id="978a3-532">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="978a3-533">(Чтобы увидеть, как она работает, когда все работает правильно, можно убрать комментарий к оператору в этом примере.)</span><span class="sxs-lookup"><span data-stu-id="978a3-533">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="978a3-534">Если код не обработал исключение, появится страница ошибки, как на предыдущем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="978a3-534">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="978a3-535">Однако раздел `try/catch` помогает предотвратить возникновение ошибок такого типа.</span><span class="sxs-lookup"><span data-stu-id="978a3-535">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="978a3-536">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="978a3-536">Additional Resources</span></span>

<span data-ttu-id="978a3-537">**Программирование с помощью Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="978a3-537">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="978a3-538">Приложение. Visual Basic язык и синтаксис</span><span class="sxs-lookup"><span data-stu-id="978a3-538">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="978a3-539">**Справочная документация**</span><span class="sxs-lookup"><span data-stu-id="978a3-539">**Reference Documentation**</span></span>

[<span data-ttu-id="978a3-540">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="978a3-540">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="978a3-541">C#Языке</span><span class="sxs-lookup"><span data-stu-id="978a3-541">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
