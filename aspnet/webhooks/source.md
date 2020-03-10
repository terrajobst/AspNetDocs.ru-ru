---
uid: webhooks/source
title: ASP.NET веб-перехватчики и пакеты NuGet | Документация Майкрософт
author: rick-anderson
description: Ссылки на исходный код веб-перехватчиков ASP.NET и пакеты NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513912"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="76bc7-103">ASP.NET веб-перехватчики, исходный код и пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="76bc7-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="76bc7-104">Microsoft ASP.NET веб-перехватчики входят в Microsoft ASP.NET семейства модулей и размещаются в виде проекта с [открытым исходным кодом на сайте GitHub](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="76bc7-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="76bc7-105">Это означает, что мы принимаем вклады, но перед отправкой запроса на вытягивание ознакомьтесь с [рекомендациями по публикации](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) .</span><span class="sxs-lookup"><span data-stu-id="76bc7-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="76bc7-106">Эта интерактивная документация, которую вы читаете сейчас, также размещена [на сайте GitHub в виде открытого кода](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) , а также принимает вклады.</span><span class="sxs-lookup"><span data-stu-id="76bc7-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="76bc7-107">Пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="76bc7-107">NuGet packages</span></span>

<span data-ttu-id="76bc7-108">[Пакеты NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) делятся на три части:</span><span class="sxs-lookup"><span data-stu-id="76bc7-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="76bc7-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common)— общий пакет, который совместно используется отправителями и получателями.</span><span class="sxs-lookup"><span data-stu-id="76bc7-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="76bc7-110">[Отправитель](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): набор пакетов, поддерживающих отправку собственных веб-перехватчиков другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="76bc7-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="76bc7-111">Функция отправки веб-перехватчиков более подробно описана в разделе [отправляются](sending/senders.md)вызовы.</span><span class="sxs-lookup"><span data-stu-id="76bc7-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="76bc7-112">[Получатели](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): набор пакетов, поддерживающих получение веб-перехватчиков от других.</span><span class="sxs-lookup"><span data-stu-id="76bc7-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="76bc7-113">Дополнительные сведения о возможностях получения веб-перехватчиков [см. в](receiving/index.md)этой статье.</span><span class="sxs-lookup"><span data-stu-id="76bc7-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
