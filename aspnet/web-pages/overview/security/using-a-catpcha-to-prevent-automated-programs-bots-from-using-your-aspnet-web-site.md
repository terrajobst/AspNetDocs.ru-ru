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
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>Использование CAPTCHA для предотвращения использования программы-роботы на сайте ASP.NET Web Razor)

по [Майкрософт](https://github.com/microsoft)

> В этой статье объясняется, как использовать ReCaptcha (мера безопасности), чтобы предотвратить выполнение задач на веб-сайте веб-страницы ASP.NET (Razor) автоматизированными программами (программы-роботы).
> 
> **Что вы узнаете:** 
> 
> - Добавление теста CAPTCHA на сайт.
> 
> Это функции ASP.NET, представленные в статье:
> 
> - Вспомогательный метод `ReCaptcha`.
> 
> > [!NOTE]
> > Сведения в этой статье относятся к веб-страницы ASP.NET 1,0 и веб-страницам 2.

## <a name="about-captchas"></a>О Каптчас

Каждый раз, когда вы разрешите регистрацию пользователей на сайте или просто вводите имя и URL-адрес (например, в комментарий блога), вы можете получить перегрузку фиктивных имен. Часто они отображаются автоматическими программами (программы-роботы), которые пытаются оставить URL-адреса на каждом веб-сайте, который они могут найти. (Распространенная мотивация заключается в публикации URL-адресов продуктов для продажи.)

Вы можете убедиться, что пользователь является реальным лицом, а не компьютерной программой, используя *CAPTCHA* для проверки пользователей при регистрации или в противном случае ввести их имя и сайт. CAPTCHA означает полностью автоматизированный открытый тест Turing для информирования компьютеров и людей друг от друга. CAPTCHA — это тест с *запросом и ответом* , в котором пользователю предлагается сделать что-то легко, но для этого достаточно сложно выполнить автоматизированную программу. Наиболее распространенным типом CAPTCHA является то, что вы видите несколько искаженных букв и запрашиваете их ввод. (Искажение должно заставить программы-роботы расшифровать буквы.)

## <a name="adding-a-recaptcha-test"></a>Добавление теста ReCaptcha

На страницах ASP.NET можно использовать вспомогательный метод `ReCaptcha` для отображения теста CAPTCHA, основанного на службе ReCaptcha ([http://recaptcha.net](http://recaptcha.net)). В вспомогательном приложении `ReCaptcha` отображается изображение двух искаженных слов, которые пользователи должны правильно ввести перед проверкой страницы. Ответ пользователя проверяется службой ReCaptcha.Net.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Зарегистрируйте свой веб-сайт по адресу ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)). После завершения регистрации вы получите открытый ключ и закрытый ключ.
2. Добавьте библиотеку вспомогательных веб-функций ASP.NET на веб-сайт, как описано в разделе [Установка вспомогательных функций на веб-страницы ASP.net сайте](https://go.microsoft.com/fwlink/?LinkId=252372), если вы этого еще не сделали.
3. Если у вас еще нет файла *\_AppStart. cshtml* , в корневой папке веб-сайта создайте файл с именем *\_AppStart. cshtml*.
4. Добавьте следующие `Recaptcha` вспомогательные параметры в файл *\_AppStart. cshtml* : 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. Задайте свойства `PublicKey` и `PrivateKey` с помощью собственных открытых и закрытых ключей.
6. Сохраните файл *\_AppStart. cshtml* и закройте его.
7. В корневой папке веб-сайта создайте новую страницу с именем *reCAPTCHA. cshtml*.
8. Замените имеющееся содержимое следующим: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. Запустите страницу *reCAPTCHA. cshtml* в браузере. Если значение `PrivateKey` является допустимым, на странице отображается элемент управления ReCaptcha и кнопка. Если вы не настроили ключи глобально в *\_AppStart. HTML*, на странице отобразится сообщение об ошибке. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. Введите слова для теста. Если вы пройдете тест ReCaptcha, появится сообщение с этим результатом. В противном случае отображается сообщение об ошибке, и элемент управления ReCaptcha отображается повторно.

> [!NOTE]
> Если компьютер находится в домене, использующем прокси-сервер, может потребоваться настроить элемент `defaultproxy` файла *Web. config* . В следующем примере показан файл *Web. config* с элементом `defaultproxy`, настроенным для обеспечения работы службы reCAPTCHA.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Дополнительные ресурсы

- [Настройка поведения сайта для сайтов веб-страницы ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202906)
- [Сайт ReCaptcha](https://www.google.com/recaptcha)
