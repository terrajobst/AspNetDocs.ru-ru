---
uid: webhooks/receiving/dependencies
title: Зависимости приемника веб-перехватчиков ASP.NET | Документация Майкрософт
author: rick-anderson
description: Зависимости получателя и внедрение зависимостей в веб-перехватчики ASP.NET.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564874"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>Зависимости получателя веб-перехватчиков ASP.NET

Microsoft ASP.NET веб-перехватчиков разрабатывается с учетом внедрения зависимостей. Большинство зависимостей в системе можно заменить альтернативными реализациями с помощью подсистемы внедрения зависимостей.

Список зависимостей получателей см. в разделе [депенденцископикстенсионс](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) . Если зависимости не зарегистрированы, используется реализация по умолчанию. Список реализаций по умолчанию см. в разделе [рецеиверсервицес](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) .
