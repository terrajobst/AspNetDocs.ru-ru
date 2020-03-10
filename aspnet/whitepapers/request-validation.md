---
uid: whitepapers/request-validation
title: Проверка запросов — предотвращение атак сценариев | Документация Майкрософт
author: rick-anderson
description: В этом документе описывается функция проверки запросов ASP.NET, где, по умолчанию, приложению запрещено обрабатывать незакодированное содержимое HTML субмитт...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520584"
---
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="0bf09-103">Проверка запроса. Предотвращение атак на основе сценариев</span><span class="sxs-lookup"><span data-stu-id="0bf09-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="0bf09-104">В этом документе описывается функция проверки запросов ASP.NET, где, по умолчанию, приложению запрещено обрабатывать незакодированное HTML-содержимое, отправленное на сервер.</span><span class="sxs-lookup"><span data-stu-id="0bf09-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="0bf09-105">Эта функция проверки запросов может быть отключена, если приложение предназначено для безопасной обработки данных HTML.</span><span class="sxs-lookup"><span data-stu-id="0bf09-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="0bf09-106">Применяется к ASP.NET 1,1 и ASP.NET 2,0.</span><span class="sxs-lookup"><span data-stu-id="0bf09-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="0bf09-107">Проверка запросов — это функция ASP.NET (начиная с версии 1.1), блокирующая прием содержимого с незашифрованным HTML-кодом на сервере.</span><span class="sxs-lookup"><span data-stu-id="0bf09-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="0bf09-108">Эта функция помогает предотвращать некоторые атаки путем внедрения кода, с помощью которых злоумышленники могут оправлять неизвестный код скрипта клиента или HTML-код на сервер, сохранять его, а затем распространять другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="0bf09-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="0bf09-109">Мы настоятельно рекомендуем при необходимости проверять все входные данные и кодировать их в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="0bf09-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="0bf09-110">Например, вы создаете веб-страницу, которая запрашивает адрес электронной почты пользователя, а затем сохраняет этот адрес электронной почты в базе данных.</span><span class="sxs-lookup"><span data-stu-id="0bf09-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="0bf09-111">Если пользователь вводит &lt;сценарий&gt;предупреждения ("Привет из скрипта")&lt;/SCRIPT&gt; вместо допустимого адреса электронной почты, этот скрипт можно выполнить, если содержимое не было закодировано должным образом.</span><span class="sxs-lookup"><span data-stu-id="0bf09-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="0bf09-112">Функция проверки запросов ASP.NET не позволяет это делать.</span><span class="sxs-lookup"><span data-stu-id="0bf09-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="0bf09-113">Почему эта функция полезна</span><span class="sxs-lookup"><span data-stu-id="0bf09-113">Why this feature is useful</span></span>

<span data-ttu-id="0bf09-114">Многие сайты не знают о том, что они открыты для простых атак путем внедрения сценариев.</span><span class="sxs-lookup"><span data-stu-id="0bf09-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="0bf09-115">Следует ли использовать эти атаки для нарушить сайт, отображая HTML, или, возможно, выполнить клиентский сценарий для перенаправления пользователя на веб-сайт хакера, атаки путем внедрения сценариев — это проблема, с которой разработчики должны конкурировать.</span><span class="sxs-lookup"><span data-stu-id="0bf09-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="0bf09-116">Атаки путем внедрения сценариев являются проблемой для всех веб-разработчиков, будь то использование ASP.NET, ASP или других технологий веб-разработки.</span><span class="sxs-lookup"><span data-stu-id="0bf09-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="0bf09-117">Функция проверки запросов ASP.NET заранее предотвращает эти атаки, запрещая обработку незакодированного HTML-содержимого сервером, если только разработчик не решил разрешить это содержимое.</span><span class="sxs-lookup"><span data-stu-id="0bf09-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="0bf09-118">Что следует предполагать: страница ошибки</span><span class="sxs-lookup"><span data-stu-id="0bf09-118">What to expect: Error Page</span></span>

<span data-ttu-id="0bf09-119">На снимке экрана ниже показан пример кода ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="0bf09-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="0bf09-120">Выполнение этого кода приводит к отображению простой страницы, которая позволяет ввести некоторый текст в текстовое поле, нажать кнопку и отобразить текст в элементе управления Label:</span><span class="sxs-lookup"><span data-stu-id="0bf09-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="0bf09-121">Однако были бы JavaScript, например `<script>alert("hello!")</script>` для введения и отправки, мы получаем исключение:</span><span class="sxs-lookup"><span data-stu-id="0bf09-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="0bf09-122">В сообщении об ошибке указывается, что обнаружено потенциально опасное значение запроса. форма, а также подробные сведения о том, что именно произошло и как изменить поведение.</span><span class="sxs-lookup"><span data-stu-id="0bf09-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="0bf09-123">Пример:</span><span class="sxs-lookup"><span data-stu-id="0bf09-123">For example:</span></span>

<span data-ttu-id="0bf09-124">При проверке запроса обнаружено потенциально опасное входное значение клиента, а обработка запроса была прервана.</span><span class="sxs-lookup"><span data-stu-id="0bf09-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="0bf09-125">Это значение может означать попытку нарушения безопасности приложения, например атаки с помощью межсайтовых сценариев.</span><span class="sxs-lookup"><span data-stu-id="0bf09-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="0bf09-126">Проверку запроса можно отключить, задав `validateRequest=false` в директиве Page или в разделе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0bf09-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="0bf09-127">Однако настоятельно рекомендуется, чтобы приложение явно проверит все входные данные в этом случае.</span><span class="sxs-lookup"><span data-stu-id="0bf09-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="0bf09-128">Отключение проверки запросов на странице</span><span class="sxs-lookup"><span data-stu-id="0bf09-128">Disabling request validation on a page</span></span>

<span data-ttu-id="0bf09-129">Чтобы отключить проверку запросов на странице, необходимо задать для атрибута `validateRequest` директивы страницы значение `false`:</span><span class="sxs-lookup"><span data-stu-id="0bf09-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="0bf09-130">Если проверка запросов отключена, содержимое можно отправить на страницу. разработчик страницы обязан обеспечить правильную кодировку и обработку содержимого.</span><span class="sxs-lookup"><span data-stu-id="0bf09-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="0bf09-131">Отключение проверки запросов для приложения</span><span class="sxs-lookup"><span data-stu-id="0bf09-131">Disabling request validation for your application</span></span>

<span data-ttu-id="0bf09-132">Чтобы отключить проверку запросов для приложения, необходимо изменить или создать файл Web. config для приложения и задать для атрибута validateRequest раздела `<pages />` значение `false`.</span><span class="sxs-lookup"><span data-stu-id="0bf09-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="0bf09-133">Если вы хотите отключить проверку запросов для всех приложений на сервере, можно внести это изменение в файл Machine. config.</span><span class="sxs-lookup"><span data-stu-id="0bf09-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="0bf09-134">Если проверка запросов отключена, содержимое можно отправить в приложение. разработчик приложения обязан обеспечить правильную кодировку и обработку содержимого.</span><span class="sxs-lookup"><span data-stu-id="0bf09-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="0bf09-135">Приведенный ниже код изменен для отключения проверки запроса.</span><span class="sxs-lookup"><span data-stu-id="0bf09-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="0bf09-136">Теперь, если следующий код JavaScript был добавлен в текстовое поле `<script>alert("hello!")</script>` результат будет следующим:</span><span class="sxs-lookup"><span data-stu-id="0bf09-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="0bf09-137">Чтобы избежать этого, при отключенной проверке запросов необходимо кодировать содержимое в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="0bf09-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="0bf09-138">Как кодировать содержимое в формате HTML</span><span class="sxs-lookup"><span data-stu-id="0bf09-138">How to HTML encode content</span></span>

<span data-ttu-id="0bf09-139">Если проверка запросов отключена, рекомендуется использовать HTML-кодирование содержимого, которое будет храниться для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="0bf09-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="0bf09-140">Кодировка HTML автоматически заменит все "&lt;" или "&gt;" (вместе с несколькими другими символами) на соответствующее представление в кодировке HTML.</span><span class="sxs-lookup"><span data-stu-id="0bf09-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="0bf09-141">Например, "&lt;" заменяется на "&amp;lt;", а "&gt;" заменяется на "&amp;gt;".</span><span class="sxs-lookup"><span data-stu-id="0bf09-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="0bf09-142">Браузеры используют эти специальные коды для вывода "&lt;" или "&gt;" в браузере.</span><span class="sxs-lookup"><span data-stu-id="0bf09-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="0bf09-143">Содержимое может быть легко закодировано в формате HTML на сервере с помощью `Server.HtmlEncode(string)` API.</span><span class="sxs-lookup"><span data-stu-id="0bf09-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="0bf09-144">Содержимое также можно легко декодировать в формате HTML, то есть вернуться к стандартному HTML-коду с помощью метода `Server.HtmlDecode(string)`.</span><span class="sxs-lookup"><span data-stu-id="0bf09-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="0bf09-145">Результат:</span><span class="sxs-lookup"><span data-stu-id="0bf09-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)
