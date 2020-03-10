---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Масштабирование SignalR с помощью служебной шины Azure | Документация Майкрософт
author: bradygaster
description: Версии программного обеспечения, используемые в этом разделе, Visual Studio 2013 .NET 4,5 SignalR версии 2 предыдущих версий этого раздела для версии SignalR 1. x этой статьи,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467736"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a>Масштабирование SignalR с помощью служебной шины Azure

по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

В этом руководстве вы развернете приложение SignalR в веб-роли Windows Azure, используя объединительную плату служебной шины для распространения сообщений на каждый экземпляр роли. (Вы также можете использовать объединительную плату служебной шины с [веб-приложениями в службе приложений Azure](https://docs.microsoft.com/azure/app-service-web/).)

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

Предварительные требования:

- Учетная запись Windows Azure.
- [Пакет Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).
- Visual Studio 2012 или 2013.

Объединительная плата служебной шины также совместима с [служебной шиной для Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)версии 1,1. Однако она несовместима с Service Bus версии 1,0 для Windows Server.

## <a name="pricing"></a>Цены

Объединительная плата служебной шины использует разделы для отправки сообщений. Последние сведения о ценах см. в статье [служебная шина](https://azure.microsoft.com/pricing/details/service-bus/). На момент написания этой статьи вы можете отправить 1 000 000 сообщений в месяц для менее $1. Объединительная плата отправляет сообщение служебной шины для каждого вызова метода концентратора SignalR. Кроме того, существуют некоторые управляющие сообщения для соединений, отключений, объединения или покидает группы и т. д. В большинстве приложений большая часть трафика сообщений будет вызывать метод концентратора.

## <a name="overview"></a>Обзор

Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.

1. Создайте новое пространство имен служебной шины с помощью портал Azure Windows.
2. Добавьте следующие пакеты NuGet в приложение: 

    - [Microsoft. AspNet. SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. ASPNET. SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) или [Microsoft. AspNet. SignalR. servicebus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)
3. Создание приложения SignalR.
4. Добавьте следующий код в Startup.cs, чтобы настроить объединительную плату: 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

Этот код настраивает для объединительной платы значения по умолчанию для [топиккаунт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) и [макскуеуеленгс](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx). Сведения об изменении этих значений см. в разделе [производительность SignalR: метрики масштабирования](signalr-performance.md#scaleout_metrics).

Для каждого приложения выберите другое значение для параметра "YourAppName". Не используйте одинаковое значение в нескольких приложениях.

## <a name="create-the-azure-services"></a>Создание служб Azure

Создайте облачную службу, как описано в статье [Создание и развертывание облачной службы](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy). Выполните действия, описанные в разделе "как создать облачную службу с помощью быстрого создания". В этом руководстве не требуется отправлять сертификат.

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

Создайте новое пространство имен служебной шины, как описано в разделе [Использование разделов и подписок служебной шины](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions). Выполните действия, описанные в разделе "Создание пространства имен службы".

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> Обязательно выберите один и тот же регион для облачной службы и пространства имен служебной шины.

## <a name="create-the-visual-studio-project"></a>Создание проекта Visual Studio

Запустите среду Visual Studio. В меню **Файл** выберите **Новый проект**.

В диалоговом окне **Новый проект** разверните узел **визуальный C#** элемент. В разделе **Установленные шаблоны**выберите **облако** , а затем выберите **облачная служба Windows Azure**. Примите значение по умолчанию .NET Framework 4,5. Присвойте приложению имя Чатсервице и нажмите кнопку **ОК**.

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

В диалоговом окне **новая облачная служба Windows Azure** выберите ASP.NET веб-роль. Нажмите кнопку со стрелкой вправо ( **&gt;** ), чтобы добавить роль в решение.

Наведите указатель мыши на новую роль, чтобы увидеть значок карандаша. Щелкните этот значок, чтобы переименовать роль. Присвойте роли имя "Сигналрчат" и нажмите кнопку **ОК**.

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

В диалоговом окне **Новый проект ASP.NET** выберите **MVC**и нажмите кнопку ОК.

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

Мастер проектов создает два проекта:

- Чатсервице: этот проект является приложением Windows Azure. Он определяет роли Azure и другие параметры конфигурации.
- Сигналрчат: этот проект является проектом ASP.NET MVC 5.

## <a name="create-the-signalr-chat-application"></a>Создание приложения разговора SignalR

Чтобы создать приложение для разговора, выполните действия, описанные в руководстве [Начало работы с SignalR и MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).

Используйте NuGet для установки необходимых библиотек. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне **консоли диспетчера пакетов** введите следующие команды:

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

Используйте параметр `-ProjectName`, чтобы установить пакеты в проект MVC ASP.NET, а не в проект Windows Azure.

## <a name="configure-the-backplane"></a>Настройка объединительной платы

В файл Startup.cs приложения добавьте следующий код:

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

Теперь необходимо получить строку подключения к служебной шине. В портал Azure выберите созданное пространство имен служебной шины и щелкните значок ключа доступа.

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

Скопируйте строку подключения в буфер обмена, а затем вставьте ее в переменную *ConnectionString* .

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>Развертывание в Azure

В обозреватель решений разверните папку **роли** в проекте чатсервице.

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

Щелкните правой кнопкой мыши роль Сигналрчат и выберите пункт **Свойства**. Перейдите на вкладку **Конфигурация** . В разделе **экземпляры** выберите 2. Можно также задать размер виртуальной машины **очень маленький**.

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

Сохраните изменения.

В обозреватель решений щелкните правой кнопкой мыши проект Чатсервице. Нажмите кнопку **Опубликовать**.

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

Если вы впервые публикуете в Windows Azure, вы должны скачать свои учетные данные. В мастере **публикации** щелкните "войти для загрузки учетных данных". Будет предложено войти в портал Azure Windows и скачать файл параметров публикации.

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

Щелкните **Импорт** и выберите скачанный файл параметров публикации.

Щелкните **Далее**. В диалоговом окне **Параметры публикации** в разделе **облачная служба**выберите созданную ранее облачную службу.

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

Щелкните **Опубликовать**. Развертывание приложения и запуск виртуальных машин может занять несколько минут.

Теперь при запуске приложения для разговора экземпляры роли обмениваются данными через служебную шину Azure, используя раздел служебной шины. Раздел — это очередь сообщений, которая разрешает несколько подписчиков.

Объединительная плата автоматически создает раздел и подписки. Чтобы просмотреть подписки и действия с сообщениями, откройте портал Azure, выберите пространство имен служебной шины и щелкните "разделы".

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

Отображение действия сообщения на панели мониторинга займет несколько минут.

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

SignalR управляет временем существования раздела. Пока приложение развернуто, не пытайтесь вручную удалить разделы или изменить параметры в разделе.

## <a name="troubleshooting"></a>Устранение неполадок

**System. InvalidOperationException "единственным поддерживаемым IsolationLevel является" IsolationLevel. Serializable ".**

Эта ошибка может возникать, если на уровне транзакции для операции задано значение, отличное от `Serializable`. Убедитесь, что никакие операции не выполняются с другими уровнями транзакций.
