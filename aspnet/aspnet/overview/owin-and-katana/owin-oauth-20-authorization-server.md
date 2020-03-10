---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: Сервер авторизации OWIN OAuth 2,0 | Документация Майкрософт
author: hongyes
description: Из этого руководства вы узнаете, как реализовать сервер авторизации OAuth 2,0 с помощью по промежуточного слоя OWIN OAuth. Это расширенный учебник, в котором только аутлин...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 39c78ee57f791a94af7a5fb66c3ac42d7239760f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500238"
---
# <a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="f5b19-104">Сервер авторизации OAuth 2.0 OWIN</span><span class="sxs-lookup"><span data-stu-id="f5b19-104">OWIN OAuth 2.0 Authorization Server</span></span>

<span data-ttu-id="f5b19-105">[Платформа OAuth 2,0](http://tools.ietf.org/html/rfc6749) позволяет сторонним приложениям получить ограниченный доступ к службе HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5b19-105">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="f5b19-106">Вместо того чтобы использовать учетные данные владельца ресурса для доступа к защищенному ресурсу, клиент получает маркер доступа (строка, обозначающая конкретную область, время существования и другие атрибуты доступа).</span><span class="sxs-lookup"><span data-stu-id="f5b19-106">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="f5b19-107">Маркеры доступа выдаются сторонним клиентам с помощью сервера авторизации с утверждением владельца ресурса.</span><span class="sxs-lookup"><span data-stu-id="f5b19-107">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="f5b19-108">OWIN определяет стандартный интерфейс между веб-серверами и веб-приложениями .NET.</span><span class="sxs-lookup"><span data-stu-id="f5b19-108">OWIN defines a standard interface between .NET web servers and web applications.</span></span> <span data-ttu-id="f5b19-109">Целью интерфейса OWIN является отделение сервера и приложения, поддержка разработки простых модулей для разработки веб-приложений .NET и, как открытый стандарт, стимулировать экосистему с открытым исходным кодом средств разработки веб-приложений .NET.</span><span class="sxs-lookup"><span data-stu-id="f5b19-109">The goal of the OWIN interface is to decouple server and application, encourage the development of simple modules for .NET web development, and, by being an open standard, stimulate the open source ecosystem of .NET web development tools.</span></span>

<span data-ttu-id="f5b19-110">Дополнительные сведения см. в разделе [OWIN](http://owin.org/)</span><span class="sxs-lookup"><span data-stu-id="f5b19-110">For more information, see [OWIN](http://owin.org/)</span></span>
