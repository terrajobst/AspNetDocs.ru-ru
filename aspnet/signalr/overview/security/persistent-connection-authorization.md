---
uid: signalr/overview/security/persistent-connection-authorization
title: Проверка подлинности и авторизация для постоянных подключений SignalR | Документация Майкрософт
author: bradygaster
description: В этом разделе описывается принудительное применение авторизации для постоянного подключения. Общие сведения об интеграции безопасности в приложение SignalR,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467478"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a>Проверка подлинности и авторизация для постоянных подключений SignalR

[Патрик Флетчера](https://github.com/pfletcher), [Tom фитзмаккен](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом разделе описывается принудительное применение авторизации для постоянного подключения. Общие сведения о интеграции безопасности в приложение SignalR см. [в статье Введение в безопасность](introduction-to-security.md).
>
> ## <a name="software-versions-used-in-this-topic"></a>Версии программного обеспечения, используемые в этом разделе
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR версии 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Предыдущие версии этого раздела
>
> Сведения о более ранних версиях SignalR см. в статье о [старых версиях](../older-versions/index.md)SignalR.
>
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
>
> Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы. Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).

## <a name="enforce-authorization"></a>Принудительная авторизация

Чтобы применить правила авторизации при использовании [персистентконнектион](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , необходимо переопределить метод `AuthorizeRequest`. Нельзя использовать атрибут `Authorize` с постоянными соединениями. Метод `AuthorizeRequest` вызывается платформой SignalR перед каждым запросом, чтобы убедиться, что пользователь имеет право выполнять запрошенное действие. Метод `AuthorizeRequest` не вызывается из клиента; Вместо этого выполняется проверка подлинности пользователя с помощью стандартного механизма проверки подлинности приложения.

В приведенном ниже примере показано, как ограничить запросы для пользователей, прошедших проверку подлинности.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

В метод AuthorizeRequest можно добавить любую настраиваемую логику авторизации. Например, проверка принадлежности пользователя к определенной роли.
