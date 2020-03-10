---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: Использование OWIN для самостоятельного размещения веб-API ASP.NET-ASP.NET 4. x
author: rick-anderson
description: Руководство с кодом, демонстрирующим размещение веб-API ASP.NET в консольном приложении.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448332"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a>Использование OWIN для самостоятельного размещения веб-API ASP.NET 

> В этом руководстве показано, как разместить веб-API ASP.NET в консольном приложении, используя OWIN для самостоятельного размещения платформы веб-API.
>
> [Открытый веб-интерфейс для .NET](http://owin.org) (OWIN) определяет абстракцию между веб-серверами и веб-приложениями .NET. OWIN отделяет веб-приложение от сервера, что делает OWIN идеальным для самостоятельного размещения веб-приложения в собственном процессе вне служб IIS.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - 5\.2.7 веб-API

> [!NOTE]
> Полный исходный код для этого руководства можно найти по адресу [GitHub.com/ASPNET/Samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).

## <a name="create-a-console-application"></a>Создание консольного приложение

В меню **файл** выберите **создать**, а затем выберите **проект**. В **разделе** **C#Visual**выберите **Рабочий стол Windows** и выберите **консольное приложение (.NET Framework)** . Присвойте проекту имя "Овинселфхостсампле" и нажмите кнопку **ОК**.

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>Добавление веб-API и пакетов OWIN

В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне "Консоль диспетчера пакетов" введите следующую команду:

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

При этом будет установлен пакет WebAPI OWIN резидент и все необходимые OWIN пакеты.

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>Настройка веб-API для самостоятельного размещения

В обозреватель решений щелкните правой кнопкой мыши проект и выберите **добавить** / **класс** , чтобы добавить новый класс. Назовите класс `Startup`.

![](use-owin-to-self-host-web-api/_static/image5.png)

Замените весь стандартный код в этом файле следующим кодом:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>Добавление контроллера веб-API

Затем добавьте класс контроллера веб-API. В обозреватель решений щелкните правой кнопкой мыши проект и выберите **добавить** / **класс** , чтобы добавить новый класс. Назовите класс `ValuesController`.

Замените весь стандартный код в этом файле следующим кодом:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>Запуск узла OWIN и создание запроса с помощью HttpClient

Замените весь стандартный код в файле Program.cs следующим кодом:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>Выполнение приложения

Чтобы запустить приложение, нажмите клавишу F5 в Visual Studio. Полученный результат должен выглядеть примерно так:

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>Дополнительные ресурсы

[Обзор проекта Katana](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Веб-API ASP.NET узла в рабочей роли Azure](host-aspnet-web-api-in-an-azure-worker-role.md)
