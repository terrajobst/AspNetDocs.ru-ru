---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: Проверка подлинности и авторизация для постоянных подключений SignalR (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается принудительное применение авторизации для постоянного подключения. Общие сведения об интеграции безопасности в приложение SignalR,...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431190"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>Проверка подлинности и авторизация для постоянных подключений SignalR (SignalR 1.x)

[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом разделе описывается принудительное применение авторизации для постоянного подключения. Общие сведения о интеграции безопасности в приложение SignalR см. [в статье Введение в безопасность](index.md).

## <a name="enforce-authorization"></a>Принудительная авторизация

Чтобы применить правила авторизации при использовании [персистентконнектион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , необходимо переопределить метод `AuthorizeRequest`. Нельзя использовать атрибут `Authorize` с постоянными соединениями. Метод `AuthorizeRequest` вызывается платформой SignalR перед каждым запросом, чтобы убедиться, что пользователь имеет право выполнять запрошенное действие. Метод `AuthorizeRequest` не вызывается из клиента; Вместо этого выполняется проверка подлинности пользователя с помощью стандартного механизма проверки подлинности приложения.

В приведенном ниже примере показано, как ограничить запросы для пользователей, прошедших проверку подлинности.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

В метод AuthorizeRequest можно добавить любую настраиваемую логику авторизации. Например, проверка принадлежности пользователя к определенной роли.
