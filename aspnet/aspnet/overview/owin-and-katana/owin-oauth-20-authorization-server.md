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
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000682"
---
# <a name="owin-oauth-20-authorization-server"></a>Сервер авторизации OAuth 2.0 OWIN

[Платформа OAuth 2,0](http://tools.ietf.org/html/rfc6749) позволяет сторонним приложениям получить ограниченный доступ к службе HTTP. Вместо того чтобы использовать учетные данные владельца ресурса для доступа к защищенному ресурсу, клиент получает маркер доступа (строка, обозначающая конкретную область, время существования и другие атрибуты доступа). Маркеры доступа выдаются сторонним клиентам с помощью сервера авторизации с утверждением владельца ресурса.

OWIN определяет стандартный интерфейс между веб-серверами и веб-приложениями .NET. Целью интерфейса OWIN является отделение сервера и приложения, поддержка разработки простых модулей для разработки веб-приложений .NET и, как открытый стандарт, стимулировать экосистему с открытым исходным кодом средств разработки веб-приложений .NET.

Дополнительные сведения см. в разделе [OWIN](http://owin.org/)
