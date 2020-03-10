---
uid: web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
title: '[Инструкции:] Реализация обработки ошибок при отправке сообщения электронной почты с помощью ASP.NET | Документация Майкрософт'
author: rick-anderson
description: Крис пикселей показывает, как реализовать обработку ошибок при отправке сообщения электронной почты с помощью ASP.NET. Он создает веб-страницу ASP.NET для отправки электронной почты, в которой показано, как настроить & lt...
ms.author: riande
ms.date: 11/06/2008
ms.assetid: c02ffd50-aa19-4cdc-b1bf-760989979a61
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
msc.type: video
ms.openlocfilehash: faa0daa2ffe71e58cd18bb8bed4e476ffcb1852e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457938"
---
# <a name="how-do-i-implement-error-handling-when-sending-email-with-aspnet"></a><span data-ttu-id="3a6ba-104">[Инструкции:] Реализация обработки ошибок при отправке сообщения электронной почты с помощью ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3a6ba-104">[How Do I:] Implement Error Handling when Sending Email with ASP.NET</span></span>

<span data-ttu-id="3a6ba-105">от [Крис пикселей](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="3a6ba-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="3a6ba-106">Крис пикселей показывает, как реализовать обработку ошибок при отправке сообщения электронной почты с помощью ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3a6ba-106">Chris Pels shows how to implement error handling when sending an email with ASP.NET.</span></span> <span data-ttu-id="3a6ba-107">Он создает веб-страницу ASP.NET для отправки электронной почты, показывает, как настроить &lt;Маилсеттингс&gt; в файле Web. config, описывает класс System .NET. mail и то, как он используется для создания и отправки сообщений электронной почты.</span><span class="sxs-lookup"><span data-stu-id="3a6ba-107">He creates an ASP.NET web page to send email, shows how to configure &lt;mailSettings&gt; in the web.config file, describes the System.Net.Mail class and how it's used to create and send email messages.</span></span> <span data-ttu-id="3a6ba-108">Затем он добавляет обработку ошибок с помощью классов исключений System .NET. mail, которые предоставляют сведения об ошибках, которые могут возникать при отправке электронной почты, и просматривает перечисление SmtpStatusCode, которое предоставляет список возможных результатов при отправке сообщения электронной почты с помощью SmtpClient.</span><span class="sxs-lookup"><span data-stu-id="3a6ba-108">He then adds error handling using System.Net.Mail exception classes, which provide information about errors that can occur when sending email, and reviews the SmtpStatusCode enumeration, which provides a list of possible outcomes when sending an email with the SmtpClient.</span></span> <span data-ttu-id="3a6ba-109">Наконец, он отправляет тестовое сообщение, которое вызывает исключение и проверяет сведения об обработке ошибок в отладчике Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a6ba-109">Finally, he sends a test email that raises an exception and reviews the error handling information in the Visual Studio debugger.</span></span>

[<span data-ttu-id="3a6ba-110">&#9654;Смотреть видео (24 минуты)</span><span class="sxs-lookup"><span data-stu-id="3a6ba-110">&#9654; Watch video (24 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-error-handling-when-sending-email-with-aspnet)
