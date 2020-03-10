---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Примеры Katana | Документация Майкрософт
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472350"
---
# <a name="katana-samples"></a>Примеры Katana

по [Майкрософт](https://github.com/microsoft)

## <a name="katana-samples"></a>Примеры Katana

Пример [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes) | **маршрутов ASP.NET**  
В некоторых приложениях необходимо подключать компоненты OWIN в таблице маршрутизации Asp.Net параллельно с компонентами, отличными от OWIN. В этом примере показано, как использовать методы расширения RouteCollection Маповинпас и Маповинрауте, предоставляемые Microsoft. Owin. host. SystemWeb.

**Пример конвейеров ветвления** | [исходном коде](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
Конвейеры обработки запросов OWIN не должны быть линейными, они могут быть разветвлены для обработки запросов различными способами. В этом примере показано, как создать конвейер ветвления на основе путей запросов или других данных запроса, таких как заголовки. Эти компоненты доступны в пакете NuGet Microsoft. Owin. mapping.

**Пользовательский пример** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) сервера   
Показывает, как использовать пользовательский сервер OWIN при размещении OWIN.

**Внедренный пример** [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded) |   
Некоторые серверы OWIN можно запускать в собственном процессе (&quot;локально размещенном&quot;). В этом примере показано, как запустить приложение OWIN с помощью средств, предоставляемых пакетом NuGet Microsoft. Owin. Hosting.

**HelloWorld** . пример [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld) |   
OWIN — это абстракция API HTTP-сервера, обеспечивающая переносимость приложений на различных серверах. В этом образце показано, как написать приложение Hello World с помощью **простых оболочек** , связанных с необработанной абстракцией OWIN, и запустить ее на веб-сервере, например ASP.NET.

**Hello World необработанного примера** [ИСХОДНОГО кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin) | OWIN  
В этом примере показано, как написать приложение Hello World с помощью **необработанной** абстракции OWIN и запустить его на веб-сервере, например ASP.NET.

**Пример** [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR) SignalR |   
Показывает, как самостоятельно размещать SignalR с помощью OWIN/Katana. Дополнительные сведения о самостоятельном размещении SignalR см. в разделе [учебник. Саморазмещение SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

**Статический файл пример** | [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
Показывает, как поддерживать HTTP-запросы для статических файлов с помощью OWIN/Katana.

[Исходный код](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) | **веб-API**   
В этом примере показано, как разместить OWIN в IIS и добавить веб-API в конвейер OWIN.

Пример [исходного кода](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) **веб-сокета** |    
Показывает, как поддерживать веб-сокеты в OWIN с помощью класса [System .NET. WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) .
