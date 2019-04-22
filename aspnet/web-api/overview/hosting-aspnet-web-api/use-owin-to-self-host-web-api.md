---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: Использование OWIN для резидентного размещения ASP.NET Web API — ASP.NET 4.x
author: rick-anderson
description: Учебник, код, показывающий, как разместить веб-API ASP.NET в консольном приложении.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: a67db0bd061846af2db3599e0843ed7c6a22db1e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59386519"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a>Использование OWIN для резидентного размещения веб-API ASP.NET 


> Этом руководстве показано, как разместить веб-API ASP.NET в консольном приложении, с помощью OWIN для резидентного размещения платформа веб-API.
>
> [Открыть веб-интерфейс .NET](http://owin.org) (OWIN) определяет абстракции между веб-серверов .NET и веб-приложений. OWIN отделяет веб-приложения на сервер, который идеально OWIN для резидентного размещения веб-приложения в собственном процессе, за пределами служб IIS.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - Веб-API 5.2.7


> [!NOTE]
> Полный исходный код для выполнения инструкций этого руководства можно найти [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).


## <a name="create-a-console-application"></a>Создание консольного приложения

На **файл** меню **New**, а затем выберите **проекта**. Из **установленные**в разделе **Visual C#** выберите **Windows Desktop** , а затем выберите **консольное приложение (.Net Framework)**. Присвойте проекту имя «OwinSelfhostSample» и выберите **ОК**.

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>Добавьте пакеты веб-API и OWIN

Из **средства** меню, выберите **диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне консоли диспетчера пакетов введите следующую команду:

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

Это установит пакет selfhost OWIN веб-API и все необходимые пакеты OWIN.

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>Настройка веб-API для резидентного размещения

В обозревателе решений щелкните правой кнопкой мыши проект и выберите **добавить** / **класс** для добавления нового класса. Присвойте классу имя `Startup`.

![](use-owin-to-self-host-web-api/_static/image5.png)

Замените весь код шаблона в этом файле следующим кодом:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>Добавление контроллера веб-API

Добавьте класс контроллера веб-API. В обозревателе решений щелкните правой кнопкой мыши проект и выберите **добавить** / **класс** для добавления нового класса. Присвойте классу имя `ValuesController`.

Замените весь код шаблона в этом файле следующим кодом:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>Запустите хоста OWIN и сделать запрос с помощью HttpClient

Замените весь код шаблона в файле Program.cs следующим кодом:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>Запуск приложения

Чтобы запустить приложение, нажмите клавишу F5 в Visual Studio. Этот вывод должен выглядеть так:

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>Дополнительные ресурсы

[Обзор проекта Katana](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Размещение веб-API ASP.NET в рабочей роли Azure](host-aspnet-web-api-in-an-azure-worker-role.md)
