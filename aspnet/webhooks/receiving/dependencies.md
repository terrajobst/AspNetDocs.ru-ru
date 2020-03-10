---
uid: webhooks/receiving/dependencies
title: Зависимости приемника веб-перехватчиков ASP.NET | Документация Майкрософт
author: rick-anderson
description: Зависимости получателя и внедрение зависимостей в веб-перехватчики ASP.NET.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517530"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="8e2c2-103">Зависимости получателя веб-перехватчиков ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8e2c2-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="8e2c2-104">Microsoft ASP.NET веб-перехватчиков разрабатывается с учетом внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="8e2c2-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="8e2c2-105">Большинство зависимостей в системе можно заменить альтернативными реализациями с помощью подсистемы внедрения зависимостей.</span><span class="sxs-lookup"><span data-stu-id="8e2c2-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="8e2c2-106">Список зависимостей получателей см. в разделе [депенденцископикстенсионс](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) .</span><span class="sxs-lookup"><span data-stu-id="8e2c2-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="8e2c2-107">Если зависимости не зарегистрированы, используется реализация по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e2c2-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="8e2c2-108">Список реализаций по умолчанию см. в разделе [рецеиверсервицес](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) .</span><span class="sxs-lookup"><span data-stu-id="8e2c2-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
