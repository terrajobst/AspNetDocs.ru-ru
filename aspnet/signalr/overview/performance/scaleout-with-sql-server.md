---
uid: signalr/overview/performance/scaleout-with-sql-server
title: Масштабирование SignalR с помощью SQL Server | Документация Майкрософт
author: bradygaster
description: Версии программного обеспечения, используемые в этом разделе, Visual Studio 2013 .NET 4,5 SignalR версии 2 в предыдущих версиях этого раздела для получения сведений о более ранних версиях...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467742"
---
# <a name="signalr-scaleout-with-sql-server"></a>Масштабирование SignalR с помощью SQL Server

по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

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

В этом руководстве вы будете использовать SQL Server для распространения сообщений в приложении SignalR, которое развернуто в двух отдельных экземплярах IIS. Вы также можете запустить этот учебник на одном тестовом компьютере, но чтобы получить полный результат, необходимо развернуть приложение SignalR на двух или более серверах. Необходимо также установить SQL Server на одном из серверов или на отдельном выделенном сервере. Другой вариант — Запустить руководство с помощью виртуальных машин в Azure.

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>предварительные требования

Microsoft SQL Server 2005 или более поздней версии. Объединительная плата поддерживает как настольные, так и серверные версии SQL Server. Он не поддерживает SQL Server Compact выпуска или базу данных SQL Azure. (Если приложение размещено в Azure, вместо него следует рассмотреть объединительную плату служебной шины.)

## <a name="overview"></a>Обзор

Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.

1. Создайте новую пустую базу данных. Объединительная плата создаст необходимые таблицы в этой базе данных.
2. Добавьте следующие пакеты NuGet в приложение:

    - [Microsoft. AspNet. SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. AspNet. SignalR. SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. Создание приложения SignalR.
4. Добавьте следующий код в Startup.cs, чтобы настроить объединительную плату:

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   Этот код настраивает для объединительной платы значения по умолчанию для [таблекаунт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) и [макскуеуеленгс](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx). Сведения об изменении этих значений см. в разделе [производительность SignalR: метрики масштабирования](signalr-performance.md#scaleout_metrics).

## <a name="configure-the-database"></a>Настройка базы данных

Определите, будет ли приложение использовать проверку подлинности Windows или проверку подлинности SQL Server для доступа к базе данных. В любом случае убедитесь, что пользователь базы данных имеет разрешения на вход, создание схем и создание таблиц.

Создайте новую базу данных для использования с объединительной платой. Можно присвоить базе данных любое имя. Не нужно создавать таблицы в базе данных; Объединительная плата создаст необходимые таблицы.

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>Включить Service Broker

Рекомендуется включить Service Broker для базы данных объединительной платы. Service Broker обеспечивает собственную поддержку обмена сообщениями и очередей в SQL Server, что позволяет повысить эффективность получения обновлений на объединительной плате. (Однако задняя панель также работает без Service Broker.)

Чтобы проверить, включена ли Service Broker, запросите столбец **\_Broker\_включен** в представлении каталога **sys. databases** .

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

Чтобы включить Service Broker, используйте следующий запрос SQL:

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> Если этот запрос выглядит как взаимоблокировка, убедитесь, что к базе данных не подключено ни одного приложения.

Если трассировка включена, трассировки также показывают, включена ли Service Broker.

## <a name="create-a-signalr-application"></a>Создание приложения SignalR

Создайте приложение SignalR, следуя одному из следующих учебников:

- [Начало работы с SignalR 2,0](../getting-started/tutorial-getting-started-with-signalr.md)
- [Начало работы с SignalR 2,0 и MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

Далее мы изменим приложение разговора для поддержки масштабирования с SQL Server. Сначала добавьте в проект пакет NuGet SignalR. SqlServer. В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

Затем откройте файл Startup.cs. Добавьте следующий код в метод **Configure** :

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>Развертывание и запуск приложения

Подготовьте экземпляры Windows Server к развертыванию приложения SignalR.

Добавьте роль IIS. Включите функции разработки приложений, включая протокол WebSocket.

![](scaleout-with-sql-server/_static/image4.png)

Также включите службу управления (указанную в разделе "средства управления").

![](scaleout-with-sql-server/_static/image5.png)

**Установите веб-развертывание 3,0.** При запуске диспетчера IIS будет предложено установить веб-платформу Майкрософт, или вы можете [скачать установщик](https://go.microsoft.com/fwlink/?LinkId=255386). В установщике платформы найдите веб-развертывание и установите веб-развертывание 3,0.

![](scaleout-with-sql-server/_static/image6.png)

Убедитесь, что служба веб-управления запущена. В противном случае запустите службу. (Если служба веб-управления не отображается в списке служб Windows, убедитесь, что служба управления установлена при добавлении роли IIS.)

Наконец, откройте порт 8172 для TCP. Это порт, используемый средством веб-развертывание.

Теперь все готово для развертывания проекта Visual Studio с компьютера разработки на сервере. В обозреватель решений щелкните решение правой кнопкой мыши и выберите пункт **опубликовать**.

Более подробную документацию по веб-развертыванию см. в разделе [веб-развертывание Map Web для Visual Studio и ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).

При развертывании приложения на двух серверах можно открыть каждый экземпляр в отдельном окне браузера и увидеть, что каждый из них получает сообщения SignalR от другого. (Конечно, в рабочей среде два сервера будут находиться за подсистемой балансировки нагрузки.)

![](scaleout-with-sql-server/_static/image7.png)

После запуска приложения вы увидите, что SignalR автоматически создал таблицы в базе данных:

![](scaleout-with-sql-server/_static/image8.png)

SignalR управляет таблицами. Пока приложение развернуто, не удаляйте строки, модифицируйте таблицу и т. д.
