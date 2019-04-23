---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[Инструкции] Отправка сообщения электронной почты, асинхронно с помощью ASP.NET | Документация Майкрософт'
author: rick-anderson
description: В этом видео Крис Пелз показано, как использовать классы System.Net.Mail в ASP.NET для отправки сообщения электронной почты асинхронной. Во-первых см. в разделе Настройка веб-сайт...
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: ea29823446cc1339003160bd3e945bde1af42473
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59421372"
---
# <a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="c721a-104">[Инструкции] Отправка сообщения электронной почты, асинхронно с помощью ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c721a-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>

<span data-ttu-id="c721a-105">по [Крис Пелз](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="c721a-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="c721a-106">В этом видео Крис Пелз показано, как использовать классы System.Net.Mail в ASP.NET для отправки сообщения электронной почты асинхронной.</span><span class="sxs-lookup"><span data-stu-id="c721a-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="c721a-107">Во-первых, см. в разделе Настройка веб-сайта для отправки электронной почты с помощью &lt;mailSettings&gt; в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="c721a-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="c721a-108">Создайте простой пользовательский интерфейс для ввода данных электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c721a-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="c721a-109">Затем вы научитесь создавать класс MailMessage используется для создания сообщения электронной почты в коде программной части для страницы.</span><span class="sxs-lookup"><span data-stu-id="c721a-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="c721a-110">В рамках этого процесса, создайте обработчик событий для асинхронный обратный вызов после отправки сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c721a-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="c721a-111">В событии обработчик см. в разделе способа использования экземпляра класса AsynchCompletedEventArgs, который предоставляет сведения о отправки электронной почты, процесс.</span><span class="sxs-lookup"><span data-stu-id="c721a-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="c721a-112">Наконец отправить тестовое электронное сообщение асинхронно, выполнив действия, описанные в режиме отладки и Просмотр фактического сообщения, полученные из процесса.</span><span class="sxs-lookup"><span data-stu-id="c721a-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="c721a-113">&#9654;Просмотрите видео (18 минут)</span><span class="sxs-lookup"><span data-stu-id="c721a-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
