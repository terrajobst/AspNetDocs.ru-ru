---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Общие сведения о веб-программировании ASP.NET с использованием синтаксиса Razor (Visual Basic) | Документация Майкрософт
author: Rick-Anderson
description: В этом приложении содержатся общие сведения о программировании с помощью веб-страниц ASP.NET в Visual Basic с использованием синтаксис Razor.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422664"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="33f40-103">Введение в веб-программирование на ASP.NET с помощью синтаксиса Razor (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="33f40-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="33f40-104">от [Tom фитзмаккен](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="33f40-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="33f40-105">В этой статье приводятся общие сведения о программировании с помощью веб-страницы ASP.NET синтаксис Razor и Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="33f40-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="33f40-106">ASP.NET — это технология корпорации Майкрософт для запуска динамических веб-страниц на веб-серверах.</span><span class="sxs-lookup"><span data-stu-id="33f40-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="33f40-107">**Что вы**узнаете:</span><span class="sxs-lookup"><span data-stu-id="33f40-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="33f40-108">8 лучших советов по программированию для начинающих веб-страницы ASP.NET с помощью синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="33f40-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="33f40-109">Основные понятия программирования, которые вам понадобятся.</span><span class="sxs-lookup"><span data-stu-id="33f40-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="33f40-110">Что ASP.NET серверный код и синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="33f40-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="33f40-111">Версии программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="33f40-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="33f40-112">Веб-страницы ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="33f40-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="33f40-113">Этот учебник также работает с веб-страницы ASP.NET 2.</span><span class="sxs-lookup"><span data-stu-id="33f40-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="33f40-114">В большинстве примеров использования веб-страницы ASP.NET с синтаксис Razor C#.</span><span class="sxs-lookup"><span data-stu-id="33f40-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="33f40-115">Но синтаксис Razor также поддерживает Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="33f40-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="33f40-116">Чтобы программировать веб-страницу ASP.NET в Visual Basic, создайте веб-страницу с расширением *. vbhtml* , а затем добавьте код Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="33f40-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="33f40-117">В этой статье приводятся общие сведения о работе с языком Visual Basic и синтаксисом для создания веб-страниц ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="33f40-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="33f40-118">Шаблоны веб-сайтов по умолчанию для Microsoft WebMatrix (**кондитерской** **, фотоальбом и** **начальный сайт**и т. д.) C# доступны в и Visual Basic версиях.</span><span class="sxs-lookup"><span data-stu-id="33f40-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="33f40-119">Шаблоны Visual Basic можно установить в виде пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="33f40-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="33f40-120">Шаблоны веб-сайтов устанавливаются в корневую папку сайта в папке с именем *Microsoft Templates*.</span><span class="sxs-lookup"><span data-stu-id="33f40-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="33f40-121">8 лучших советов по программированию</span><span class="sxs-lookup"><span data-stu-id="33f40-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="33f40-122">В этом разделе приведено несколько советов, которые необходимо знать при написании кода сервера ASP.NET с помощью синтаксис Razor.</span><span class="sxs-lookup"><span data-stu-id="33f40-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="33f40-123">1. Вы добавляете код на страницу с помощью символа @.</span><span class="sxs-lookup"><span data-stu-id="33f40-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="33f40-124">`@` символ начинается со встроенных выражений, блоков одной инструкции и многооператорных блоков:</span><span class="sxs-lookup"><span data-stu-id="33f40-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="33f40-125">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-125">The result displayed in a browser:</span></span>

![Razor — Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="33f40-127">**Кодировка HTML**</span><span class="sxs-lookup"><span data-stu-id="33f40-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="33f40-128">При отображении содержимого на странице с помощью `@` символа, как в предыдущих примерах, ASP.NET HTML кодирует выходные данные.</span><span class="sxs-lookup"><span data-stu-id="33f40-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="33f40-129">Это заменяет зарезервированные символы HTML (например, `<` и `>` и `&`) кодами, которые позволяют отображать символы в виде символов на веб-странице, а не интерпретировать их как теги HTML или сущности.</span><span class="sxs-lookup"><span data-stu-id="33f40-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="33f40-130">Без кодирования HTML выходные данные из кода сервера могут отображаться неправильно, и может представлять угрозу безопасности страницы.</span><span class="sxs-lookup"><span data-stu-id="33f40-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="33f40-131">Если ваша цель — вывод HTML-разметки, которая отображает теги как разметку (например `<p></p>` для абзаца или `<em></em>`, чтобы подчеркнуть текст), см. раздел [Объединение текста, разметки и кода в блоках кода](#BM_CombiningTextMarkupAndCode) ниже в этой статье.</span><span class="sxs-lookup"><span data-stu-id="33f40-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="33f40-132">Дополнительные сведения о кодировке HTML см. в статье как [работать с HTML-формами на веб-страницы ASP.NET сайтах](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="33f40-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="33f40-133">2. Вы заключаете блоки кода в код... Конечный код</span><span class="sxs-lookup"><span data-stu-id="33f40-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="33f40-134">Блок кода включает один или несколько операторов кода, заключенный в ключевые слова `Code` и `End Code`.</span><span class="sxs-lookup"><span data-stu-id="33f40-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="33f40-135">Поместите ключевое слово Open `Code` сразу после `@` символа &#8212; , между которыми не может быть пробел.</span><span class="sxs-lookup"><span data-stu-id="33f40-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="33f40-136">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-136">The result displayed in a browser:</span></span>

![Razor — Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="33f40-138">3. внутри блока все операторы кода завершаются разрывом строки</span><span class="sxs-lookup"><span data-stu-id="33f40-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="33f40-139">В блоке кода Visual Basic каждая инструкция заканчивается разрывом строки.</span><span class="sxs-lookup"><span data-stu-id="33f40-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="33f40-140">(Далее в статье вы увидите способ заключения длинной инструкции Code в несколько строк, если это необходимо.)</span><span class="sxs-lookup"><span data-stu-id="33f40-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="33f40-141">4. переменные используются для хранения значений</span><span class="sxs-lookup"><span data-stu-id="33f40-141">4. You use variables to store values</span></span>

<span data-ttu-id="33f40-142">Значения можно хранить в *переменной*, включая строки, числа и даты и т. д. Новую переменную можно создать с помощью ключевого слова `Dim`.</span><span class="sxs-lookup"><span data-stu-id="33f40-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="33f40-143">Значения переменных можно вставлять непосредственно на странице с помощью `@`.</span><span class="sxs-lookup"><span data-stu-id="33f40-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="33f40-144">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-144">The result displayed in a browser:</span></span>

![Razor — Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="33f40-146">5. строковые литеральные значения заключаются в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="33f40-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="33f40-147">*Строка* представляет собой последовательность символов, обрабатываемых как текст.</span><span class="sxs-lookup"><span data-stu-id="33f40-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="33f40-148">Чтобы указать строку, заключите ее в двойные кавычки:</span><span class="sxs-lookup"><span data-stu-id="33f40-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="33f40-149">Чтобы внедрить двойные кавычки в строковое значение, вставьте два символа двойной кавычки.</span><span class="sxs-lookup"><span data-stu-id="33f40-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="33f40-150">Если требуется, чтобы символ двойной кавычки отображался один раз в выходных данных страницы, введите его как `""` в строке в кавычках и, если нужно, чтобы он выглядел дважды, введите его как `""""` в строке в кавычках.</span><span class="sxs-lookup"><span data-stu-id="33f40-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="33f40-151">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-151">The result displayed in a browser:</span></span>

![Razor — Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="33f40-153">6. Visual Basic код не чувствителен к регистру</span><span class="sxs-lookup"><span data-stu-id="33f40-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="33f40-154">Язык Visual Basic не чувствителен к регистру.</span><span class="sxs-lookup"><span data-stu-id="33f40-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="33f40-155">Ключевые слова программирования (такие как `Dim`, `If`и `True`) и имена переменных (например, `myString`или `subTotal`) могут быть написаны в любом случае.</span><span class="sxs-lookup"><span data-stu-id="33f40-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="33f40-156">Следующие строки кода присваивают значение переменной `lastname` используя имя в нижнем регистре, а затем выводят значение переменной на страницу, используя имя в верхнем регистре.</span><span class="sxs-lookup"><span data-stu-id="33f40-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="33f40-157">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-157">The result displayed in a browser:</span></span>

![VB — синтаксис – 5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="33f40-159">7. большая часть кода предполагает работу с объектами</span><span class="sxs-lookup"><span data-stu-id="33f40-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="33f40-160">Объект представляет вещь, которую можно программировать с &#8212; помощью страницы, текстового поля, файла, изображения, веб-запроса, сообщения электронной почты, записи клиента (строки базы данных) и т. д. Объекты имеют свойства, описывающие их &#8212; характеристики объект текстового поля имеет свойство `Text`, объект запроса имеет свойство `Url`, сообщение электронной почты имеет свойство `From`, а объект Customer имеет свойство `FirstName`.</span><span class="sxs-lookup"><span data-stu-id="33f40-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="33f40-161">Объекты также имеют методы, которые являются &quot;командами&quot; они могут выполняться.</span><span class="sxs-lookup"><span data-stu-id="33f40-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="33f40-162">К примерам относятся метод `Save` файлового объекта, метод `Rotate` объекта изображения и метод `Send` объекта сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="33f40-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="33f40-163">Часто приходится работать с объектом `Request`, который предоставляет сведения, такие как значения полей формы на странице (текстовые поля и т. д.), тип браузера, который выполнил запрос, URL-адрес страницы, удостоверение пользователя и т. д. В этом примере показано, как получить доступ к свойствам объекта `Request` и вызвать метод `MapPath` объекта `Request`, который предоставляет абсолютный путь к странице на сервере:</span><span class="sxs-lookup"><span data-stu-id="33f40-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="33f40-164">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-164">The result displayed in a browser:</span></span>

![Razor — Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="33f40-166">8. можно написать код, который принимает решения</span><span class="sxs-lookup"><span data-stu-id="33f40-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="33f40-167">Ключевой функцией динамических веб-страниц является то, что вы можете определить, что делать на основе условий.</span><span class="sxs-lookup"><span data-stu-id="33f40-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="33f40-168">Самый распространенный способ сделать это — с помощью оператора `If` (и необязательной инструкции `Else`).</span><span class="sxs-lookup"><span data-stu-id="33f40-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="33f40-169">`If IsPost` инструкции — это сокращенный способ написания `If IsPost = True`.</span><span class="sxs-lookup"><span data-stu-id="33f40-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="33f40-170">Наряду с инструкциями `If` существует множество способов проверки условий, повторных блоков кода и т. д., которые описаны далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="33f40-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="33f40-171">Результат, отображаемый в браузере (после нажатия кнопки **Отправить**):</span><span class="sxs-lookup"><span data-stu-id="33f40-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor — Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="33f40-173">**Методы HTTP GET и POST и свойство POST**</span><span class="sxs-lookup"><span data-stu-id="33f40-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="33f40-174">Протокол, используемый для веб-страниц (HTTP), поддерживает очень ограниченное число методов (&quot;глаголы&quot;), которые используются для выполнения запросов к серверу.</span><span class="sxs-lookup"><span data-stu-id="33f40-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="33f40-175">Двумя наиболее распространенными являются GET, который используется для чтения страницы, и POST, который используется для отправки страницы.</span><span class="sxs-lookup"><span data-stu-id="33f40-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="33f40-176">В общем случае при первом запросе страницы пользователем страница запрашивается с помощью GET.</span><span class="sxs-lookup"><span data-stu-id="33f40-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="33f40-177">Если пользователь заполняет форму и нажимает кнопку **Отправить**, браузер ОТПРАВЛЯЕТ запрос POST на сервер.</span><span class="sxs-lookup"><span data-stu-id="33f40-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="33f40-178">В веб-программировании часто бывает полезно определить, запрашивается ли страница как GET или AS POST, чтобы вы узнали, как обрабатывать страницу.</span><span class="sxs-lookup"><span data-stu-id="33f40-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="33f40-179">В веб-страницы ASP.NET можно использовать свойство `IsPost`, чтобы определить, является ли запрос сообщением GET или POST.</span><span class="sxs-lookup"><span data-stu-id="33f40-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="33f40-180">Если запрос является POST, свойство `IsPost` возвратит значение true, и вы можете выполнять такие действия, как чтение значений текстовых полей в форме.</span><span class="sxs-lookup"><span data-stu-id="33f40-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="33f40-181">Во многих примерах вы увидите, как обрабатывать страницу по-разному в зависимости от значения `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="33f40-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="33f40-182">Простой пример кода</span><span class="sxs-lookup"><span data-stu-id="33f40-182">A Simple Code Example</span></span>

<span data-ttu-id="33f40-183">В этой процедуре показано, как создать страницу, на которой показаны основные методики программирования.</span><span class="sxs-lookup"><span data-stu-id="33f40-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="33f40-184">В этом примере создается страница, позволяющая пользователям вводить два числа, затем добавляет их и отображает результат.</span><span class="sxs-lookup"><span data-stu-id="33f40-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="33f40-185">В редакторе создайте новый файл и назовите его *подставлял. vbhtml*.</span><span class="sxs-lookup"><span data-stu-id="33f40-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="33f40-186">Скопируйте приведенный ниже код и разметку на страницу, заменив все, что уже есть на странице.</span><span class="sxs-lookup"><span data-stu-id="33f40-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="33f40-187">Обратите внимание на некоторые моменты.</span><span class="sxs-lookup"><span data-stu-id="33f40-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="33f40-188">`@` символ запускает первый блок кода на странице, и он предшествует `totalMessage` переменной, внедренной в нижнюю часть.</span><span class="sxs-lookup"><span data-stu-id="33f40-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="33f40-189">Блок в верхней части страницы заключается в `Code...End Code`.</span><span class="sxs-lookup"><span data-stu-id="33f40-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="33f40-190">Переменные `total`, `num1`, `num2`и `totalMessage` хранят несколько чисел и строку.</span><span class="sxs-lookup"><span data-stu-id="33f40-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="33f40-191">Литеральное строковое значение, присваиваемое переменной `totalMessage`, заключено в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="33f40-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="33f40-192">Поскольку в Visual Basicном коде не учитывается регистр, если в нижней части страницы используется `totalMessage` переменная, ее имя должно соответствовать только написанию объявления переменной в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="33f40-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="33f40-193">Регистр не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="33f40-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="33f40-194">Выражение `num1.AsInt()` + `num2.AsInt()` показывает, как работать с объектами и методами.</span><span class="sxs-lookup"><span data-stu-id="33f40-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="33f40-195">Метод `AsInt` для каждой переменной преобразует строку, введенную пользователем, в целое число (Integer), которое можно добавить.</span><span class="sxs-lookup"><span data-stu-id="33f40-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="33f40-196">Тег `<form>` содержит атрибут `method="post"`.</span><span class="sxs-lookup"><span data-stu-id="33f40-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="33f40-197">Это указывает, что при нажатии пользователем кнопки **Добавить**страница будет отправлена на сервер с помощью метода HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="33f40-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="33f40-198">При отправке страницы код `If IsPost` оценивается как true и выполняется условный код, отображая результат сложения чисел.</span><span class="sxs-lookup"><span data-stu-id="33f40-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="33f40-199">Сохраните страницу и запустите ее в браузере.</span><span class="sxs-lookup"><span data-stu-id="33f40-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="33f40-200">(Перед выполнением страницы убедитесь, что она выбрана в рабочей области **файлы** .) Введите два целых числа и нажмите кнопку " **Добавить** ".</span><span class="sxs-lookup"><span data-stu-id="33f40-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor — Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="33f40-202">Язык и синтаксис Visual Basic</span><span class="sxs-lookup"><span data-stu-id="33f40-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="33f40-203">Ранее вы увидели простой пример создания веб-страницы ASP.NET, а также способ добавления серверного кода в разметку HTML.</span><span class="sxs-lookup"><span data-stu-id="33f40-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="33f40-204">Здесь вы узнаете об основах использования Visual Basic для написания кода сервера ASP.NET, используя синтаксис Razor &#8212; , то есть правила языка программирования.</span><span class="sxs-lookup"><span data-stu-id="33f40-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="33f40-205">При работе с программированием (особенно если вы использовали C, C++, C#, Visual Basic или JavaScript), многие из которых вы прочитаете здесь, будут знакомы.</span><span class="sxs-lookup"><span data-stu-id="33f40-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="33f40-206">Возможно, вам потребуется ознакомиться только с тем, как код WebMatrix добавляется к разметке в файлах *. vbhtml* .</span><span class="sxs-lookup"><span data-stu-id="33f40-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a><span data-ttu-id="33f40-207">Объединение текста, разметки и кода в блоках кода</span><span class="sxs-lookup"><span data-stu-id="33f40-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="33f40-208">В блоках кода сервера часто требуется выводить текст и разметку на страницу.</span><span class="sxs-lookup"><span data-stu-id="33f40-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="33f40-209">Если блок кода сервера содержит текст, который не является кодом и, вместо этого, он должен быть отображен как есть, ASP.NET должен иметь возможность отличать этот текст от кода.</span><span class="sxs-lookup"><span data-stu-id="33f40-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="33f40-210">Это можно сделать несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="33f40-210">There are several ways to do this.</span></span>

- <span data-ttu-id="33f40-211">Заключите текст в элемент блока HTML, например `<p></p>` или `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="33f40-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="33f40-212">Элемент HTML может включать текст, дополнительные HTML-элементы и выражения серверного кода.</span><span class="sxs-lookup"><span data-stu-id="33f40-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="33f40-213">Когда ASP.NET видит открывающий HTML-тег (например, `<p>`), он отображает все элементы и его содержимое в браузере (и разрешает выражения серверного кода).</span><span class="sxs-lookup"><span data-stu-id="33f40-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="33f40-214">Используйте оператор `@:` или элемент `<text>`.</span><span class="sxs-lookup"><span data-stu-id="33f40-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="33f40-215">`@:` выводит одну строку содержимого, содержащую обычный текст или несовпадающие теги HTML; элемент `<text>` включает несколько строк для вывода.</span><span class="sxs-lookup"><span data-stu-id="33f40-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="33f40-216">Эти параметры полезны, если не нужно отображать HTML-элемент как часть выходных данных.</span><span class="sxs-lookup"><span data-stu-id="33f40-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="33f40-217">В следующем примере предыдущий пример повторяется, но используется одна пара тегов `<text>` для заключения отображаемого текста.</span><span class="sxs-lookup"><span data-stu-id="33f40-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="33f40-218">В следующем примере Теги `<text>` и `</text>` заключают три строки, все из которых содержат неавтономный текст и непарные теги HTML (`<br />`) вместе с серверным кодом и соответствующими тегами HTML.</span><span class="sxs-lookup"><span data-stu-id="33f40-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="33f40-219">Опять же, можно также предшествовать каждой строке отдельно с помощью оператора `@:`. в любом случае это работает.</span><span class="sxs-lookup"><span data-stu-id="33f40-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="33f40-220">При выводе текста, как показано в этом &#8212; разделе, с помощью элемента html, `@:` оператор или `<text>` элемент &#8212; ASP.NET не кодирует выходные данные в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="33f40-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="33f40-221">(Как отмечалось ранее, ASP.NET кодирует выходные данные выражений серверного кода и серверных блоков кода, которым предшествуют `@`, за исключением особых случаев, указанных в этом разделе.)</span><span class="sxs-lookup"><span data-stu-id="33f40-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="33f40-222">Пробел</span><span class="sxs-lookup"><span data-stu-id="33f40-222">Whitespace</span></span>

<span data-ttu-id="33f40-223">Лишние пробелы в операторе (и вне строкового литерала) не влияют на инструкцию:</span><span class="sxs-lookup"><span data-stu-id="33f40-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="33f40-224">Разбиение длинных инструкций на несколько строк</span><span class="sxs-lookup"><span data-stu-id="33f40-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="33f40-225">Можно разбить длинную инструкцию кода на несколько строк, используя символ подчеркивания `_` (который в Visual Basic называется *символом продолжения*) после каждой строки кода.</span><span class="sxs-lookup"><span data-stu-id="33f40-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="33f40-226">Для разбиения оператора на следующую строку в конце строки добавьте пробел, а затем символ продолжения.</span><span class="sxs-lookup"><span data-stu-id="33f40-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="33f40-227">Продолжите выполнение инструкции на следующей строке.</span><span class="sxs-lookup"><span data-stu-id="33f40-227">Continue the statement on the next line.</span></span> <span data-ttu-id="33f40-228">Инструкции можно переносить на несколько строк, чтобы улучшить удобочитаемость.</span><span class="sxs-lookup"><span data-stu-id="33f40-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="33f40-229">Следующие инструкции равнозначны:</span><span class="sxs-lookup"><span data-stu-id="33f40-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="33f40-230">Однако нельзя заключить строку в середину строкового литерала.</span><span class="sxs-lookup"><span data-stu-id="33f40-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="33f40-231">Следующий пример не работает:</span><span class="sxs-lookup"><span data-stu-id="33f40-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="33f40-232">Чтобы объединить длинную строку, которая переносится в несколько строк, например приведенный выше код, необходимо использовать *оператор объединения* (`&`), который будет показан далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="33f40-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="33f40-233">Комментарии к коду</span><span class="sxs-lookup"><span data-stu-id="33f40-233">Code comments</span></span>

<span data-ttu-id="33f40-234">Комментарии позволяют оставлять заметки для себя или для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="33f40-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="33f40-235">Синтаксис Razor комментарии начинаются с `@*` и заканчиваются `*@`.</span><span class="sxs-lookup"><span data-stu-id="33f40-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="33f40-236">В блоках кода можно использовать синтаксис Razor комментарии или можно использовать обычный Visual Basic символ комментария, который представляет собой одинарную кавычку (`'`), предваряя каждую строку.</span><span class="sxs-lookup"><span data-stu-id="33f40-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="33f40-237">Переменные</span><span class="sxs-lookup"><span data-stu-id="33f40-237">Variables</span></span>

<span data-ttu-id="33f40-238">Переменная — это именованный объект, который используется для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="33f40-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="33f40-239">Можно назвать любые переменные, но имя должно начинаться с буквы и не может содержать пробелы или зарезервированные символы.</span><span class="sxs-lookup"><span data-stu-id="33f40-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="33f40-240">В Visual Basic, как было показано ранее, регистр букв в имени переменной не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="33f40-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="33f40-241">Переменные и типы данных</span><span class="sxs-lookup"><span data-stu-id="33f40-241">Variables and data types</span></span>

<span data-ttu-id="33f40-242">Переменная может иметь конкретный тип данных, который указывает, какой тип данных хранится в переменной.</span><span class="sxs-lookup"><span data-stu-id="33f40-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="33f40-243">Можно использовать строковые переменные, которые хранят строковые значения (например, &quot;Hello World&quot;), целочисленные переменные, в которых хранятся целые значения (например, 3 или 79), и переменные даты, которые хранят значения дат в различных форматах (например, 4/12/2012 или Март 2009).</span><span class="sxs-lookup"><span data-stu-id="33f40-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="33f40-244">И существует много других типов данных, которые можно использовать.</span><span class="sxs-lookup"><span data-stu-id="33f40-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="33f40-245">Однако для переменной не нужно указывать тип.</span><span class="sxs-lookup"><span data-stu-id="33f40-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="33f40-246">В большинстве случаев ASP.NET может определить тип в зависимости от того, как используются данные в переменной.</span><span class="sxs-lookup"><span data-stu-id="33f40-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="33f40-247">(Иногда необходимо указать тип; вы увидите примеры, в которых это верно.)</span><span class="sxs-lookup"><span data-stu-id="33f40-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="33f40-248">Чтобы объявить переменную без указания типа, используйте `Dim` плюс имя переменной (например, `Dim myVar`).</span><span class="sxs-lookup"><span data-stu-id="33f40-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="33f40-249">Чтобы объявить переменную с типом, используйте `Dim` плюс имя переменной, затем `As`, а затем имя типа (например, `Dim myVar As String`).</span><span class="sxs-lookup"><span data-stu-id="33f40-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="33f40-250">В следующем примере показаны некоторые встроенные выражения, использующие переменные на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="33f40-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="33f40-251">Результат отображается в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-251">The result displayed in a browser:</span></span>

![Razor — Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="33f40-253">Преобразование и тестирование типов данных</span><span class="sxs-lookup"><span data-stu-id="33f40-253">Converting and testing data types</span></span>

<span data-ttu-id="33f40-254">Хотя ASP.NET обычно может определять тип данных автоматически, иногда он не может.</span><span class="sxs-lookup"><span data-stu-id="33f40-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="33f40-255">Таким образом, может потребоваться помочь ASP.NET, выполнив явное преобразование.</span><span class="sxs-lookup"><span data-stu-id="33f40-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="33f40-256">Даже если нет необходимости в преобразовании типов, иногда полезно проверить, какие типы данных могут быть вам доступны.</span><span class="sxs-lookup"><span data-stu-id="33f40-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="33f40-257">Наиболее распространенным случаем является преобразование строки в другой тип, например в Integer или Date.</span><span class="sxs-lookup"><span data-stu-id="33f40-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="33f40-258">В следующем примере показан типичный случай, когда необходимо преобразовать строку в число.</span><span class="sxs-lookup"><span data-stu-id="33f40-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="33f40-259">Как правило, вводимые пользователем данные поступают в виде строк.</span><span class="sxs-lookup"><span data-stu-id="33f40-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="33f40-260">Даже если вы предоставили пользователю запрос на ввод числа, и даже если он вводил цифру, при отправке пользовательского ввода и считывании его в коде данные представлены в строковом формате.</span><span class="sxs-lookup"><span data-stu-id="33f40-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="33f40-261">Поэтому необходимо преобразовать строку в число.</span><span class="sxs-lookup"><span data-stu-id="33f40-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="33f40-262">В этом примере, если вы попытаетесь выполнить арифметические действия со значениями без их преобразования, выдается следующее сообщение об ошибке, так как ASP.NET не может добавить две строки:</span><span class="sxs-lookup"><span data-stu-id="33f40-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="33f40-263">Чтобы преобразовать значения в целые числа, вызовите метод `AsInt`.</span><span class="sxs-lookup"><span data-stu-id="33f40-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="33f40-264">Если преобразование выполнено успешно, можно добавить числа.</span><span class="sxs-lookup"><span data-stu-id="33f40-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="33f40-265">В следующей таблице перечислены некоторые распространенные методы преобразования и тестирования для переменных.</span><span class="sxs-lookup"><span data-stu-id="33f40-265">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="33f40-266"><strong>Метод</strong></span><span class="sxs-lookup"><span data-stu-id="33f40-266"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-267"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="33f40-267"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-268"><strong>Пример</strong></span><span class="sxs-lookup"><span data-stu-id="33f40-268"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-269">Преобразует строку, представляющую целое число (например, &quot;593&quot;) в целое число.</span><span class="sxs-lookup"><span data-stu-id="33f40-269">Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-270">Преобразует строку, такую как &quot;true&quot; или &quot;false&quot;, в логический тип.</span><span class="sxs-lookup"><span data-stu-id="33f40-270">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-271">Преобразует строку, имеющую десятичное значение, например &quot;1,3&quot; или &quot;7,439&quot;, в число с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="33f40-271">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-272">Преобразует строку, имеющую десятичное значение, например &quot;1,3&quot; или &quot;7,439&quot;, в десятичное число.</span><span class="sxs-lookup"><span data-stu-id="33f40-272">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="33f40-273">(В ASP.NET десятичное число является более точным, чем число с плавающей запятой.)</span><span class="sxs-lookup"><span data-stu-id="33f40-273">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-274">Преобразует строку, представляющую значение даты и времени, в тип `DateTime` ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="33f40-274">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-275">Преобразует любой другой тип данных в строку.</span><span class="sxs-lookup"><span data-stu-id="33f40-275">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="33f40-276">Операторы</span><span class="sxs-lookup"><span data-stu-id="33f40-276">Operators</span></span>

<span data-ttu-id="33f40-277">Оператор — это ключевое слово или символ, который сообщает ASP.NET, какой тип команды выполнять в выражении.</span><span class="sxs-lookup"><span data-stu-id="33f40-277">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="33f40-278">Visual Basic поддерживает много операторов, но для начала разработки веб-страниц ASP.NET необходимо только распознавать несколько.</span><span class="sxs-lookup"><span data-stu-id="33f40-278">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="33f40-279">В следующей таблице перечислены наиболее распространенные операторы.</span><span class="sxs-lookup"><span data-stu-id="33f40-279">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="33f40-280"><strong>Оператор</strong></span><span class="sxs-lookup"><span data-stu-id="33f40-280"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-281"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="33f40-281"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-282"><strong>Примеры</strong></span><span class="sxs-lookup"><span data-stu-id="33f40-282"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-283">Математические операторы, используемые в числовых выражениях.</span><span class="sxs-lookup"><span data-stu-id="33f40-283">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-284">Присваивание и равенство.</span><span class="sxs-lookup"><span data-stu-id="33f40-284">Assignment and equality.</span></span> <span data-ttu-id="33f40-285">В зависимости от контекста либо присваивает значение справа от оператора объекту с левой стороны, либо проверяет значения на равенство.</span><span class="sxs-lookup"><span data-stu-id="33f40-285">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-286">Неравенство.</span><span class="sxs-lookup"><span data-stu-id="33f40-286">Inequality.</span></span> <span data-ttu-id="33f40-287">Возвращает `True`, если значения не равны.</span><span class="sxs-lookup"><span data-stu-id="33f40-287">Returns `True` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-288">Меньше, больше, меньше или равно и больше или равно.</span><span class="sxs-lookup"><span data-stu-id="33f40-288">Less than, greater than, less than or equal, and greater than or equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-289">Объединение, которое используется для соединения строк.</span><span class="sxs-lookup"><span data-stu-id="33f40-289">Concatenation, which is used to join strings.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-290">Операторы инкремента и декремента, которые добавляют и вычитают 1 (соответственно) из переменной.</span><span class="sxs-lookup"><span data-stu-id="33f40-290">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-291">Оператор.</span><span class="sxs-lookup"><span data-stu-id="33f40-291">Dot.</span></span> <span data-ttu-id="33f40-292">Используется для различения объектов и их свойств и методов.</span><span class="sxs-lookup"><span data-stu-id="33f40-292">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-293">Скобки.</span><span class="sxs-lookup"><span data-stu-id="33f40-293">Parentheses.</span></span> <span data-ttu-id="33f40-294">Используется для группирования выражений, для передачи параметров методам и для доступа к членам массивов и коллекций.</span><span class="sxs-lookup"><span data-stu-id="33f40-294">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-295">Недостаточно.</span><span class="sxs-lookup"><span data-stu-id="33f40-295">Not.</span></span> <span data-ttu-id="33f40-296">Меняет значение true на false и наоборот.</span><span class="sxs-lookup"><span data-stu-id="33f40-296">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="33f40-297">Обычно используется в качестве краткого способа проверки `False` (то есть не `True`).</span><span class="sxs-lookup"><span data-stu-id="33f40-297">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        <span data-ttu-id="33f40-298">Логические и и OR, которые используются для связи условий.</span><span class="sxs-lookup"><span data-stu-id="33f40-298">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="33f40-299">Работа с путями к файлам и папкам в коде</span><span class="sxs-lookup"><span data-stu-id="33f40-299">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="33f40-300">Вы часто работаете с путями к файлам и папкам в коде.</span><span class="sxs-lookup"><span data-stu-id="33f40-300">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="33f40-301">Ниже приведен пример структуры физической папки для веб-сайта, который может отображаться на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="33f40-301">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="33f40-302">Ниже приведены некоторые основные сведения о URL-адресах и путях.</span><span class="sxs-lookup"><span data-stu-id="33f40-302">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="33f40-303">URL-адрес начинается с доменного имени (`http://www.example.com`) или имени сервера (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="33f40-303">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="33f40-304">URL-адрес соответствует физическому пути на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="33f40-304">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="33f40-305">Например, `http://myserver` может соответствовать папке *к:\вебситес\мивебсите* на сервере.</span><span class="sxs-lookup"><span data-stu-id="33f40-305">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="33f40-306">Виртуальный путь является краткой для представления путей в коде без указания полного пути.</span><span class="sxs-lookup"><span data-stu-id="33f40-306">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="33f40-307">Он включает часть URL-адреса, следующую за именем домена или сервера.</span><span class="sxs-lookup"><span data-stu-id="33f40-307">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="33f40-308">При использовании виртуальных путей можно переместить код в другой домен или сервер без необходимости обновлять пути.</span><span class="sxs-lookup"><span data-stu-id="33f40-308">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="33f40-309">Ниже приведен пример, который поможет понять различия:</span><span class="sxs-lookup"><span data-stu-id="33f40-309">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="33f40-310">Полный URL-адрес</span><span class="sxs-lookup"><span data-stu-id="33f40-310">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="33f40-311">Имя сервера</span><span class="sxs-lookup"><span data-stu-id="33f40-311">Server name</span></span> | <span data-ttu-id="33f40-312">*микомпанисервер*</span><span class="sxs-lookup"><span data-stu-id="33f40-312">*mycompanyserver*</span></span> |
| <span data-ttu-id="33f40-313">Виртуальный путь</span><span class="sxs-lookup"><span data-stu-id="33f40-313">Virtual path</span></span> | <span data-ttu-id="33f40-314">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="33f40-314">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="33f40-315">Физический путь</span><span class="sxs-lookup"><span data-stu-id="33f40-315">Physical path</span></span> | <span data-ttu-id="33f40-316">*к:\мивебситес\хуманресаурцес\компаниполици.хтм*</span><span class="sxs-lookup"><span data-stu-id="33f40-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="33f40-317">Виртуальный корень имеет значение/, как и корневой каталог диска C: \.</span><span class="sxs-lookup"><span data-stu-id="33f40-317">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="33f40-318">(Пути к виртуальным папкам всегда используют косую черту.) Виртуальный путь к папке не должен совпадать с именем физической папки. Это может быть псевдоним.</span><span class="sxs-lookup"><span data-stu-id="33f40-318">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="33f40-319">(На рабочих серверах виртуальный путь редко соответствует точному физическому пути.)</span><span class="sxs-lookup"><span data-stu-id="33f40-319">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="33f40-320">При работе с файлами и папками в коде иногда требуется ссылка на физический путь и иногда виртуальный путь в зависимости от объектов, с которыми вы работаете.</span><span class="sxs-lookup"><span data-stu-id="33f40-320">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="33f40-321">ASP.NET предоставляет следующие средства для работы с путями к файлам и папкам в коде: метод `Server.MapPath`, оператор `~` и метод `Href`.</span><span class="sxs-lookup"><span data-stu-id="33f40-321">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="33f40-322">Преобразование виртуальных в физические пути: метод Server. MapPath</span><span class="sxs-lookup"><span data-stu-id="33f40-322">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="33f40-323">Метод `Server.MapPath` Преобразует виртуальный путь (например, */дефаулт.кштмл*) в абсолютный физический путь (например, *к:\вебситес\мивебситефолдер\дефаулт.кштмл*).</span><span class="sxs-lookup"><span data-stu-id="33f40-323">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="33f40-324">Этот метод используется в любой момент, когда требуется полный физический путь.</span><span class="sxs-lookup"><span data-stu-id="33f40-324">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="33f40-325">Типичный пример — при чтении или записи текстового файла или файла изображения на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="33f40-325">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="33f40-326">Как правило, абсолютный физический путь к сайту на сервере узла размещения не известен, поэтому этот метод может преобразовать известный путь (виртуальный путь) в соответствующий путь на сервере.</span><span class="sxs-lookup"><span data-stu-id="33f40-326">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="33f40-327">Виртуальный путь передается в файл или папку в метод и возвращает физический путь:</span><span class="sxs-lookup"><span data-stu-id="33f40-327">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="33f40-328">Ссылка на виртуальный корень: оператор ~ и метод href</span><span class="sxs-lookup"><span data-stu-id="33f40-328">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="33f40-329">В файле *. cshtml* или *. vbhtml* можно ссылаться на виртуальный корневой путь с помощью оператора `~`.</span><span class="sxs-lookup"><span data-stu-id="33f40-329">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="33f40-330">Это очень удобно, так как можно перемещать страницы на сайте и любые ссылки, содержащиеся на других страницах, не будут разорваны.</span><span class="sxs-lookup"><span data-stu-id="33f40-330">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="33f40-331">Это также удобно, если вы перемещаете веб-сайт в другое место.</span><span class="sxs-lookup"><span data-stu-id="33f40-331">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="33f40-332">Ниже приведены некоторые примеры:</span><span class="sxs-lookup"><span data-stu-id="33f40-332">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="33f40-333">Если веб-сайт `http://myserver/myapp`, то, как ASP.NET будет обрабатывать эти пути при выполнении страницы:</span><span class="sxs-lookup"><span data-stu-id="33f40-333">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="33f40-334">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="33f40-334">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="33f40-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="33f40-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="33f40-336">(В действительности эти пути не отображаются как значения переменной, но ASP.NET будет рассматривать пути так, как будто они были.)</span><span class="sxs-lookup"><span data-stu-id="33f40-336">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="33f40-337">Оператор `~` можно использовать как в коде сервера (как описано выше), так и в разметке следующим образом:</span><span class="sxs-lookup"><span data-stu-id="33f40-337">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="33f40-338">В разметке оператор `~` используется для создания путей к ресурсам, таким как файлы изображений, другие веб-страницы и файлы CSS.</span><span class="sxs-lookup"><span data-stu-id="33f40-338">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="33f40-339">При запуске страницы ASP.NET просматривает страницу (как код, так и разметку) и разрешает все `~` ссылки на соответствующий путь.</span><span class="sxs-lookup"><span data-stu-id="33f40-339">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="33f40-340">Условная логика и циклы</span><span class="sxs-lookup"><span data-stu-id="33f40-340">Conditional Logic and Loops</span></span>

<span data-ttu-id="33f40-341">ASP.NET Server Code позволяет выполнять задачи на основе условий и писать код, который повторяет инструкции определенное число раз, то есть код, выполняющий цикл.</span><span class="sxs-lookup"><span data-stu-id="33f40-341">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="33f40-342">Условия тестирования</span><span class="sxs-lookup"><span data-stu-id="33f40-342">Testing conditions</span></span>

<span data-ttu-id="33f40-343">Чтобы проверить простое условие, используйте инструкцию `If...Then`, которая возвращает `True` или `False` на основе указанного теста:</span><span class="sxs-lookup"><span data-stu-id="33f40-343">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="33f40-344">Ключевое слово `If` запускает блок.</span><span class="sxs-lookup"><span data-stu-id="33f40-344">The `If` keyword starts a block.</span></span> <span data-ttu-id="33f40-345">Фактический тест (условие) следует за ключевым словом `If` и возвращает true или false.</span><span class="sxs-lookup"><span data-stu-id="33f40-345">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="33f40-346">Оператор `If` заканчивается `Then`.</span><span class="sxs-lookup"><span data-stu-id="33f40-346">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="33f40-347">Инструкции, которые будут выполняться, если тест имеет значение true, заключаются в `If` и `End If`.</span><span class="sxs-lookup"><span data-stu-id="33f40-347">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="33f40-348">Инструкция `If` может включать блок `Else`, указывающий, какие операторы выполняются, если условие ложно:</span><span class="sxs-lookup"><span data-stu-id="33f40-348">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="33f40-349">Если оператор `If` запускает блок кода, для включения блоков не нужно использовать обычные операторы `Code...End Code`.</span><span class="sxs-lookup"><span data-stu-id="33f40-349">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="33f40-350">Можно просто добавить `@` в блок, и он будет работать.</span><span class="sxs-lookup"><span data-stu-id="33f40-350">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="33f40-351">Этот подход работает с `If`, а также с другими Visual Basic ключевыми словами программирования, за которыми следуют блоки кода, включая `For`, `For Each`, `Do While`и т. д.</span><span class="sxs-lookup"><span data-stu-id="33f40-351">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="33f40-352">Можно добавить несколько условий с помощью одного или нескольких блоков `ElseIf`:</span><span class="sxs-lookup"><span data-stu-id="33f40-352">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="33f40-353">В этом примере, если первое условие в блоке `If` не равно true, проверяется `ElseIf` условие.</span><span class="sxs-lookup"><span data-stu-id="33f40-353">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="33f40-354">Если это условие выполнено, выполняются инструкции в блоке `ElseIf`.</span><span class="sxs-lookup"><span data-stu-id="33f40-354">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="33f40-355">Если ни одно из условий не соблюдается, выполняются инструкции в блоке `Else`.</span><span class="sxs-lookup"><span data-stu-id="33f40-355">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="33f40-356">Можно добавить любое количество блоков `ElseIf`, а затем закрыть блок `Else` как &quot;все остальное&quot; условие.</span><span class="sxs-lookup"><span data-stu-id="33f40-356">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="33f40-357">Чтобы проверить большое количество условий, используйте блок `Select Case`:</span><span class="sxs-lookup"><span data-stu-id="33f40-357">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="33f40-358">Проверяемое значение находится в круглых скобках (в примере это переменная Weekday).</span><span class="sxs-lookup"><span data-stu-id="33f40-358">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="33f40-359">Каждый отдельный тест использует инструкцию `Case`, в которой содержится значение.</span><span class="sxs-lookup"><span data-stu-id="33f40-359">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="33f40-360">Если значение инструкции `Case` соответствует тестовому значению, выполняется код в этом блоке `Case`.</span><span class="sxs-lookup"><span data-stu-id="33f40-360">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="33f40-361">Результат двух последних условных блоков, отображаемых в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-361">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor — Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="33f40-363">Циклическое выполнение кода</span><span class="sxs-lookup"><span data-stu-id="33f40-363">Looping code</span></span>

<span data-ttu-id="33f40-364">Часто приходится многократно выполнять одни и те же инструкции.</span><span class="sxs-lookup"><span data-stu-id="33f40-364">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="33f40-365">Для этого нужно выполнить цикл.</span><span class="sxs-lookup"><span data-stu-id="33f40-365">You do this by looping.</span></span> <span data-ttu-id="33f40-366">Например, часто выполняются одни и те же инструкции для каждого элемента в коллекции данных.</span><span class="sxs-lookup"><span data-stu-id="33f40-366">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="33f40-367">Если точно известно, сколько раз вы хотите пройти цикл, можно использовать цикл `For`.</span><span class="sxs-lookup"><span data-stu-id="33f40-367">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="33f40-368">Этот тип цикла особенно полезен для подсчета или пересчета:</span><span class="sxs-lookup"><span data-stu-id="33f40-368">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="33f40-369">Цикл начинается с ключевого слова `For`, за которым следуют три элемента:</span><span class="sxs-lookup"><span data-stu-id="33f40-369">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="33f40-370">Сразу после оператора `For` объявляется переменная счетчика (не нужно использовать `Dim`), а затем указывается диапазон, как в `i = 10 to 20`.</span><span class="sxs-lookup"><span data-stu-id="33f40-370">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="33f40-371">Это означает, что переменная `i` начнет подсчитаться 10 и продолжить до 20 (включительно).</span><span class="sxs-lookup"><span data-stu-id="33f40-371">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="33f40-372">Между операторами `For` и `Next` является содержимым блока.</span><span class="sxs-lookup"><span data-stu-id="33f40-372">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="33f40-373">Может содержать один или несколько инструкций кода, выполняемых с каждым циклом.</span><span class="sxs-lookup"><span data-stu-id="33f40-373">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="33f40-374">Оператор `Next i` завершает цикл.</span><span class="sxs-lookup"><span data-stu-id="33f40-374">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="33f40-375">Он увеличивает счетчик и запускает следующую итерацию цикла.</span><span class="sxs-lookup"><span data-stu-id="33f40-375">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="33f40-376">Строка кода между строками `For` и `Next` содержит код, который выполняется для каждой итерации цикла.</span><span class="sxs-lookup"><span data-stu-id="33f40-376">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="33f40-377">Разметка создает новый абзац (`<p>` элемент) каждый раз и добавляет строку к выходу, отображая значение i (счетчик).</span><span class="sxs-lookup"><span data-stu-id="33f40-377">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="33f40-378">При запуске этой страницы в примере создаются 11 строк, в которых отображаются выходные данные, и текст в каждой строке, указывающей на номер товара.</span><span class="sxs-lookup"><span data-stu-id="33f40-378">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor — Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="33f40-380">При работе с коллекцией или массивом часто используется цикл `For Each`.</span><span class="sxs-lookup"><span data-stu-id="33f40-380">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="33f40-381">Коллекция — это группа схожих объектов, а цикл `For Each` позволяет выполнять задачу для каждого элемента в коллекции.</span><span class="sxs-lookup"><span data-stu-id="33f40-381">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="33f40-382">Этот тип цикла удобен для коллекций, так как в отличие от цикла `For` не нужно увеличивать счетчик или устанавливать ограничение.</span><span class="sxs-lookup"><span data-stu-id="33f40-382">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="33f40-383">Вместо этого код цикла `For Each` просто проходит по коллекции, пока не завершится.</span><span class="sxs-lookup"><span data-stu-id="33f40-383">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="33f40-384">Этот пример возвращает элементы коллекции `Request.ServerVariables` (которая содержит сведения о веб-сервере).</span><span class="sxs-lookup"><span data-stu-id="33f40-384">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="33f40-385">Он использует цикл `For Each` для вывода имени каждого элемента путем создания нового элемента `<li>` в маркированном списке HTML.</span><span class="sxs-lookup"><span data-stu-id="33f40-385">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="33f40-386">За ключевым словом `For Each` следует переменная, представляющая один элемент в коллекции (в примере, `myItem`), за которой следует ключевое слово `In`, а затем Коллекция, которую необходимо прокручивать.</span><span class="sxs-lookup"><span data-stu-id="33f40-386">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="33f40-387">В теле цикла `For Each` можно получить доступ к текущему элементу с помощью объявленной ранее переменной.</span><span class="sxs-lookup"><span data-stu-id="33f40-387">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor — Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="33f40-389">Чтобы создать более общий цикл общего назначения, используйте оператор `Do While`:</span><span class="sxs-lookup"><span data-stu-id="33f40-389">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="33f40-390">Этот цикл начинается с ключевого слова `Do While`, за которым следует условие, за которым следует блок, который необходимо повторить.</span><span class="sxs-lookup"><span data-stu-id="33f40-390">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="33f40-391">Циклы обычно увеличивают (добавляются в) или уменьшают (вычитаются из) переменную или объект, используемый для подсчета.</span><span class="sxs-lookup"><span data-stu-id="33f40-391">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="33f40-392">В этом примере оператор `+=` добавляет 1 к значению переменной при каждом запуске цикла.</span><span class="sxs-lookup"><span data-stu-id="33f40-392">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="33f40-393">(Чтобы уменьшить переменную в цикле, который подсчитывается вниз, используйте оператор декремента `-=`.)</span><span class="sxs-lookup"><span data-stu-id="33f40-393">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="33f40-394">Объекты и коллекции</span><span class="sxs-lookup"><span data-stu-id="33f40-394">Objects and Collections</span></span>

<span data-ttu-id="33f40-395">Практически все на веб-сайте ASP.NET — это объект, включая саму веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="33f40-395">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="33f40-396">В этом разделе обсуждаются некоторые важные объекты, с которыми часто приходится работать в коде.</span><span class="sxs-lookup"><span data-stu-id="33f40-396">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="33f40-397">Объекты Page</span><span class="sxs-lookup"><span data-stu-id="33f40-397">Page objects</span></span>

<span data-ttu-id="33f40-398">Самым основным объектом в ASP.NET является страница.</span><span class="sxs-lookup"><span data-stu-id="33f40-398">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="33f40-399">Вы можете обращаться к свойствам объекта Page напрямую, не используя соответствующий объект.</span><span class="sxs-lookup"><span data-stu-id="33f40-399">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="33f40-400">Следующий код получает путь к файлу страницы, используя объект `Request` страницы:</span><span class="sxs-lookup"><span data-stu-id="33f40-400">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="33f40-401">Вы можете использовать свойства объекта `Page` для получения большого объема информации, например:</span><span class="sxs-lookup"><span data-stu-id="33f40-401">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="33f40-402">`Request`.</span><span class="sxs-lookup"><span data-stu-id="33f40-402">`Request`.</span></span> <span data-ttu-id="33f40-403">Как уже было показано, это коллекция сведений о текущем запросе, включая тип браузера, который сделал запрос, URL-адрес страницы, удостоверение пользователя и т. д.</span><span class="sxs-lookup"><span data-stu-id="33f40-403">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="33f40-404">`Response`.</span><span class="sxs-lookup"><span data-stu-id="33f40-404">`Response`.</span></span> <span data-ttu-id="33f40-405">Это коллекция сведений о ответе (странице), которая будет отправлена в браузер после завершения выполнения кода сервера.</span><span class="sxs-lookup"><span data-stu-id="33f40-405">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="33f40-406">Например, это свойство можно использовать для записи сведений в ответ.</span><span class="sxs-lookup"><span data-stu-id="33f40-406">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="33f40-407">Объекты коллекции (массивы и словари)</span><span class="sxs-lookup"><span data-stu-id="33f40-407">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="33f40-408">Коллекция — это группа объектов одного типа, например коллекция объектов `Customer` из базы данных.</span><span class="sxs-lookup"><span data-stu-id="33f40-408">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="33f40-409">ASP.NET содержит множество встроенных коллекций, таких как коллекция `Request.Files`.</span><span class="sxs-lookup"><span data-stu-id="33f40-409">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="33f40-410">Вы часто работаете с данными в коллекциях.</span><span class="sxs-lookup"><span data-stu-id="33f40-410">You'll often work with data in collections.</span></span> <span data-ttu-id="33f40-411">Два общих типа коллекций — это *массив* и *словарь*.</span><span class="sxs-lookup"><span data-stu-id="33f40-411">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="33f40-412">Массив полезен, если нужно сохранить коллекцию схожих элементов, но не нужно создавать отдельную переменную для хранения каждого элемента:</span><span class="sxs-lookup"><span data-stu-id="33f40-412">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="33f40-413">При использовании массивов вы объявляете конкретный тип данных, например `String`, `Integer`или `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="33f40-413">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="33f40-414">Чтобы указать, что переменная может содержать массив, добавьте круглые скобки в имя переменной в объявлении (например, `Dim myVar() As String`).</span><span class="sxs-lookup"><span data-stu-id="33f40-414">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="33f40-415">Доступ к элементам массива можно получить с помощью их позиции (индекса) или с помощью инструкции `For Each`.</span><span class="sxs-lookup"><span data-stu-id="33f40-415">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="33f40-416">Индексы массива отсчитываются от &#8212; нуля, т. е. первый элемент находится в позиции 0, второй элемент — в позиции 1 и т. д.</span><span class="sxs-lookup"><span data-stu-id="33f40-416">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="33f40-417">Чтобы определить количество элементов в массиве, можно получить свойство `Length`.</span><span class="sxs-lookup"><span data-stu-id="33f40-417">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="33f40-418">Чтобы получить позицию определенного элемента в массиве (то есть для поиска в массиве), используйте метод `Array.IndexOf`.</span><span class="sxs-lookup"><span data-stu-id="33f40-418">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="33f40-419">Можно также выполнять такие действия, как обратный порядок содержимого массива (метод `Array.Reverse`) или сортировать содержимое (метод `Array.Sort`).</span><span class="sxs-lookup"><span data-stu-id="33f40-419">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="33f40-420">Выходные данные кода массива строк, отображаемого в браузере:</span><span class="sxs-lookup"><span data-stu-id="33f40-420">The output of the string array code displayed in a browser:</span></span>

![Razor — Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="33f40-422">Словарь — это коллекция пар "ключ-значение", где вы предоставляете ключ (или имя) для установки или получения соответствующего значения:</span><span class="sxs-lookup"><span data-stu-id="33f40-422">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="33f40-423">Чтобы создать словарь, используйте ключевое слово `New`, чтобы указать, что создается новый объект `Dictionary`.</span><span class="sxs-lookup"><span data-stu-id="33f40-423">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="33f40-424">Можно назначить словарь переменной с помощью ключевого слова `Dim`.</span><span class="sxs-lookup"><span data-stu-id="33f40-424">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="33f40-425">Типы данных элементов словаря указываются с помощью круглых скобок (`( )`).</span><span class="sxs-lookup"><span data-stu-id="33f40-425">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="33f40-426">В конце объявления необходимо добавить еще одну пару круглых скобок, поскольку это фактически метод, создающий новый словарь.</span><span class="sxs-lookup"><span data-stu-id="33f40-426">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="33f40-427">Чтобы добавить элементы в словарь, можно вызвать метод `Add` переменной Dictionary (`myScores` в этом случае), а затем указать ключ и значение.</span><span class="sxs-lookup"><span data-stu-id="33f40-427">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="33f40-428">Кроме того, можно использовать круглые скобки для обозначения ключа и выполнить простое назначение, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="33f40-428">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="33f40-429">Чтобы получить значение из словаря, необходимо указать ключ в круглых скобках:</span><span class="sxs-lookup"><span data-stu-id="33f40-429">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="33f40-430">Вызов методов с параметрами</span><span class="sxs-lookup"><span data-stu-id="33f40-430">Calling Methods with Parameters</span></span>

<span data-ttu-id="33f40-431">Как было показано ранее в этой статье, объекты, с которыми Вы запрограммированы, имеют методы.</span><span class="sxs-lookup"><span data-stu-id="33f40-431">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="33f40-432">Например, объект `Database` может иметь метод `Database.Connect`.</span><span class="sxs-lookup"><span data-stu-id="33f40-432">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="33f40-433">Многие методы также имеют один или несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="33f40-433">Many methods also have one or more parameters.</span></span> <span data-ttu-id="33f40-434">*Параметр* — это значение, передаваемое в метод, чтобы позволить методу завершить свою задачу.</span><span class="sxs-lookup"><span data-stu-id="33f40-434">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="33f40-435">Например, рассмотрим объявление метода `Request.MapPath`, который принимает три параметра:</span><span class="sxs-lookup"><span data-stu-id="33f40-435">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="33f40-436">Этот метод возвращает физический путь на сервере, соответствующий указанному виртуальному пути.</span><span class="sxs-lookup"><span data-stu-id="33f40-436">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="33f40-437">Три параметра для метода: `virtualPath`, `baseVirtualDir`и `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="33f40-437">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="33f40-438">(Обратите внимание, что в объявлении указаны параметры с типами данных, которые они будут принимать.) При вызове этого метода необходимо указать значения для всех трех параметров.</span><span class="sxs-lookup"><span data-stu-id="33f40-438">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="33f40-439">Если вы используете Visual Basic с синтаксис Razor, у вас есть два варианта передачи параметров в метод: *позиционированные параметры* или *именованные параметры*.</span><span class="sxs-lookup"><span data-stu-id="33f40-439">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="33f40-440">Чтобы вызвать метод с помощью методов с параметрами, необходимо передать параметры в определенном порядке, указанном в объявлении метода.</span><span class="sxs-lookup"><span data-stu-id="33f40-440">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="33f40-441">(Обычно этот порядок вы узнаете, читая документацию по методу.) Необходимо следовать указанному порядку, и при необходимости пропустить какие-либо &#8212; параметры, передается пустая строка (`""`) или значение NULL для параметра позиционирования, для которого у вас нет значения.</span><span class="sxs-lookup"><span data-stu-id="33f40-441">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="33f40-442">В следующем примере предполагается, что на веб-сайте есть папка с именем *Scripts* .</span><span class="sxs-lookup"><span data-stu-id="33f40-442">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="33f40-443">Код вызывает метод `Request.MapPath` и передает значения для трех параметров в правильном порядке.</span><span class="sxs-lookup"><span data-stu-id="33f40-443">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="33f40-444">Затем отображается полученный сопоставленный путь.</span><span class="sxs-lookup"><span data-stu-id="33f40-444">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="33f40-445">Если для метода имеется много параметров, можно защитить код и сделать его более удобочитаемым с помощью именованных параметров.</span><span class="sxs-lookup"><span data-stu-id="33f40-445">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="33f40-446">Чтобы вызвать метод с использованием именованных параметров, укажите имя параметра, а затем `:=`, а затем укажите значение.</span><span class="sxs-lookup"><span data-stu-id="33f40-446">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="33f40-447">Преимущество именованных параметров заключается в том, что их можно добавлять в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="33f40-447">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="33f40-448">(Недостаток заключается в том, что вызов метода не является компактным.)</span><span class="sxs-lookup"><span data-stu-id="33f40-448">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="33f40-449">В следующем примере вызывается тот же метод, что и выше, но для предоставления значений используются именованные параметры:</span><span class="sxs-lookup"><span data-stu-id="33f40-449">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="33f40-450">Как видите, параметры передаются в другом порядке.</span><span class="sxs-lookup"><span data-stu-id="33f40-450">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="33f40-451">Однако если запустить предыдущий пример и этот пример, они будут возвращать одно и то же значение.</span><span class="sxs-lookup"><span data-stu-id="33f40-451">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="33f40-452">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="33f40-452">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="33f40-453">Операторы Try-Catch</span><span class="sxs-lookup"><span data-stu-id="33f40-453">Try-Catch statements</span></span>

<span data-ttu-id="33f40-454">Часто в коде есть операторы, которые могут завершиться ошибкой по причинам, находящимся за пределами элемента управления.</span><span class="sxs-lookup"><span data-stu-id="33f40-454">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="33f40-455">Пример:</span><span class="sxs-lookup"><span data-stu-id="33f40-455">For example:</span></span>

- <span data-ttu-id="33f40-456">Если код пытается открыть, создать, прочитать или записать файл, могут возникать все виды ошибок.</span><span class="sxs-lookup"><span data-stu-id="33f40-456">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="33f40-457">Возможно, нужный файл не существует, он может быть заблокирован, код может не иметь разрешений и т. д.</span><span class="sxs-lookup"><span data-stu-id="33f40-457">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="33f40-458">Аналогично, если код пытается обновить записи в базе данных, могут возникнуть проблемы с разрешениями, подключение к базе данных может быть удалено, данные для сохранения могут быть недействительными и т. д.</span><span class="sxs-lookup"><span data-stu-id="33f40-458">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="33f40-459">В терминах программирования эти ситуации называются *исключениями*.</span><span class="sxs-lookup"><span data-stu-id="33f40-459">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="33f40-460">Если код встречает исключение, он создает (выдает) сообщение об ошибке, которое, в лучшем случае, неудобно для пользователей.</span><span class="sxs-lookup"><span data-stu-id="33f40-460">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor — Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="33f40-462">В ситуациях, когда код может столкнуться с исключениями и во избежание сообщений об ошибках этого типа, можно использовать инструкции `Try/Catch`.</span><span class="sxs-lookup"><span data-stu-id="33f40-462">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="33f40-463">В инструкции `Try` выполняется проверка кода.</span><span class="sxs-lookup"><span data-stu-id="33f40-463">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="33f40-464">В одной или нескольких инструкциях `Catch` можно найти определенные ошибки (определенные типы исключений), которые могли произойти.</span><span class="sxs-lookup"><span data-stu-id="33f40-464">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="33f40-465">Можно включить столько `Catch` инструкций, сколько необходимо для поиска ожидаемых ошибок.</span><span class="sxs-lookup"><span data-stu-id="33f40-465">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="33f40-466">Рекомендуется избегать использования метода `Response.Redirect` в инструкциях `Try/Catch`, так как это может вызвать исключение на странице.</span><span class="sxs-lookup"><span data-stu-id="33f40-466">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="33f40-467">В следующем примере показана страница, которая создает текстовый файл при первом запросе, а затем отображает кнопку, которая позволяет пользователю открыть файл.</span><span class="sxs-lookup"><span data-stu-id="33f40-467">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="33f40-468">В этом примере преднамеренно используется неправильное имя файла, что вызовет исключение.</span><span class="sxs-lookup"><span data-stu-id="33f40-468">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="33f40-469">Код включает `Catch` операторы для двух возможных исключений: `FileNotFoundException`, которое происходит, если имя файла является недопустимым, и `DirectoryNotFoundException`, что происходит, если ASP.NET даже не может найти папку.</span><span class="sxs-lookup"><span data-stu-id="33f40-469">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="33f40-470">(Чтобы увидеть, как она работает, когда все работает правильно, можно убрать комментарий к оператору в этом примере.)</span><span class="sxs-lookup"><span data-stu-id="33f40-470">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="33f40-471">Если код не обработал исключение, появится страница ошибки, как на предыдущем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="33f40-471">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="33f40-472">Однако раздел `Try/Catch` помогает предотвратить возникновение ошибок такого типа.</span><span class="sxs-lookup"><span data-stu-id="33f40-472">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="33f40-473">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="33f40-473">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="33f40-474">Справочная документация</span><span class="sxs-lookup"><span data-stu-id="33f40-474">Reference Documentation</span></span>

- [<span data-ttu-id="33f40-475">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="33f40-475">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="33f40-476">Язык Visual Basic</span><span class="sxs-lookup"><span data-stu-id="33f40-476">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
