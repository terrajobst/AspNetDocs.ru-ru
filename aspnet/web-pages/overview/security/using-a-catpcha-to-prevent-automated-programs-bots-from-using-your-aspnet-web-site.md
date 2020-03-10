---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Использование CAPTCHA для предотвращения использования программы-роботы на сайте ASP.NET Web Razor) | Документация Майкрософт
author: microsoft
description: В этой статье объясняется, как использовать ReCaptcha (мера безопасности) для предотвращения выполнения задач автоматическими программами (программы-роботы) в веб-страницы ASP.NET (Razor)...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440196"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="704d7-103">Использование CAPTCHA для предотвращения использования программы-роботы на сайте ASP.NET Web Razor)</span><span class="sxs-lookup"><span data-stu-id="704d7-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="704d7-104">по [Майкрософт](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="704d7-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="704d7-105">В этой статье объясняется, как использовать ReCaptcha (мера безопасности), чтобы предотвратить выполнение задач на веб-сайте веб-страницы ASP.NET (Razor) автоматизированными программами (программы-роботы).</span><span class="sxs-lookup"><span data-stu-id="704d7-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="704d7-106">**Что вы узнаете:**</span><span class="sxs-lookup"><span data-stu-id="704d7-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="704d7-107">Добавление теста CAPTCHA на сайт.</span><span class="sxs-lookup"><span data-stu-id="704d7-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="704d7-108">Это функции ASP.NET, представленные в статье:</span><span class="sxs-lookup"><span data-stu-id="704d7-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="704d7-109">Вспомогательный метод `ReCaptcha`.</span><span class="sxs-lookup"><span data-stu-id="704d7-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="704d7-110">Сведения в этой статье относятся к веб-страницы ASP.NET 1,0 и веб-страницам 2.</span><span class="sxs-lookup"><span data-stu-id="704d7-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="704d7-111">О Каптчас</span><span class="sxs-lookup"><span data-stu-id="704d7-111">About CAPTCHAs</span></span>

<span data-ttu-id="704d7-112">Каждый раз, когда вы разрешите регистрацию пользователей на сайте или просто вводите имя и URL-адрес (например, в комментарий блога), вы можете получить перегрузку фиктивных имен.</span><span class="sxs-lookup"><span data-stu-id="704d7-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="704d7-113">Часто они отображаются автоматическими программами (программы-роботы), которые пытаются оставить URL-адреса на каждом веб-сайте, который они могут найти.</span><span class="sxs-lookup"><span data-stu-id="704d7-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="704d7-114">(Распространенная мотивация заключается в публикации URL-адресов продуктов для продажи.)</span><span class="sxs-lookup"><span data-stu-id="704d7-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="704d7-115">Вы можете убедиться, что пользователь является реальным лицом, а не компьютерной программой, используя *CAPTCHA* для проверки пользователей при регистрации или в противном случае ввести их имя и сайт.</span><span class="sxs-lookup"><span data-stu-id="704d7-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="704d7-116">CAPTCHA означает полностью автоматизированный открытый тест Turing для информирования компьютеров и людей друг от друга.</span><span class="sxs-lookup"><span data-stu-id="704d7-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="704d7-117">CAPTCHA — это тест с *запросом и ответом* , в котором пользователю предлагается сделать что-то легко, но для этого достаточно сложно выполнить автоматизированную программу.</span><span class="sxs-lookup"><span data-stu-id="704d7-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="704d7-118">Наиболее распространенным типом CAPTCHA является то, что вы видите несколько искаженных букв и запрашиваете их ввод.</span><span class="sxs-lookup"><span data-stu-id="704d7-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="704d7-119">(Искажение должно заставить программы-роботы расшифровать буквы.)</span><span class="sxs-lookup"><span data-stu-id="704d7-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="704d7-120">Добавление теста ReCaptcha</span><span class="sxs-lookup"><span data-stu-id="704d7-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="704d7-121">На страницах ASP.NET можно использовать вспомогательный метод `ReCaptcha` для отображения теста CAPTCHA, основанного на службе ReCaptcha ([http://recaptcha.net](http://recaptcha.net)).</span><span class="sxs-lookup"><span data-stu-id="704d7-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="704d7-122">В вспомогательном приложении `ReCaptcha` отображается изображение двух искаженных слов, которые пользователи должны правильно ввести перед проверкой страницы.</span><span class="sxs-lookup"><span data-stu-id="704d7-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="704d7-123">Ответ пользователя проверяется службой ReCaptcha.Net.</span><span class="sxs-lookup"><span data-stu-id="704d7-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="704d7-124">Зарегистрируйте свой веб-сайт по адресу ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span><span class="sxs-lookup"><span data-stu-id="704d7-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="704d7-125">После завершения регистрации вы получите открытый ключ и закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="704d7-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="704d7-126">Добавьте библиотеку вспомогательных веб-функций ASP.NET на веб-сайт, как описано в разделе [Установка вспомогательных функций на веб-страницы ASP.net сайте](https://go.microsoft.com/fwlink/?LinkId=252372), если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="704d7-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="704d7-127">Если у вас еще нет файла *\_AppStart. cshtml* , в корневой папке веб-сайта создайте файл с именем *\_AppStart. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="704d7-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="704d7-128">Добавьте следующие `Recaptcha` вспомогательные параметры в файл *\_AppStart. cshtml* :</span><span class="sxs-lookup"><span data-stu-id="704d7-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="704d7-129">Задайте свойства `PublicKey` и `PrivateKey` с помощью собственных открытых и закрытых ключей.</span><span class="sxs-lookup"><span data-stu-id="704d7-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="704d7-130">Сохраните файл *\_AppStart. cshtml* и закройте его.</span><span class="sxs-lookup"><span data-stu-id="704d7-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="704d7-131">В корневой папке веб-сайта создайте новую страницу с именем *reCAPTCHA. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="704d7-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="704d7-132">Замените имеющееся содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="704d7-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="704d7-133">Запустите страницу *reCAPTCHA. cshtml* в браузере.</span><span class="sxs-lookup"><span data-stu-id="704d7-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="704d7-134">Если значение `PrivateKey` является допустимым, на странице отображается элемент управления ReCaptcha и кнопка.</span><span class="sxs-lookup"><span data-stu-id="704d7-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="704d7-135">Если вы не настроили ключи глобально в *\_AppStart. HTML*, на странице отобразится сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="704d7-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="704d7-136">Введите слова для теста.</span><span class="sxs-lookup"><span data-stu-id="704d7-136">Enter the words for the test.</span></span> <span data-ttu-id="704d7-137">Если вы пройдете тест ReCaptcha, появится сообщение с этим результатом.</span><span class="sxs-lookup"><span data-stu-id="704d7-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="704d7-138">В противном случае отображается сообщение об ошибке, и элемент управления ReCaptcha отображается повторно.</span><span class="sxs-lookup"><span data-stu-id="704d7-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="704d7-139">Если компьютер находится в домене, использующем прокси-сервер, может потребоваться настроить элемент `defaultproxy` файла *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="704d7-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="704d7-140">В следующем примере показан файл *Web. config* с элементом `defaultproxy`, настроенным для обеспечения работы службы reCAPTCHA.</span><span class="sxs-lookup"><span data-stu-id="704d7-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="704d7-141">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="704d7-141">Additional Resources</span></span>

- [<span data-ttu-id="704d7-142">Настройка поведения сайта для сайтов веб-страницы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="704d7-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="704d7-143">Сайт ReCaptcha</span><span class="sxs-lookup"><span data-stu-id="704d7-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)
