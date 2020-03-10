---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: Масштабирование SignalR с SQL Server (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431130"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a>Масштабирование SignalR с помощью SQL Server (SignalR 1.x)

по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

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
4. Добавьте следующий код в Global. asax для настройки объединительной платы: 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

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

- [начало работы с SignalR](../getting-started/tutorial-getting-started-with-signalr.md)
- [начало работы с SignalR и MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)

Далее мы изменим приложение разговора для поддержки масштабирования с SQL Server. Сначала добавьте в проект пакет NuGet SignalR. SqlServer. В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

Затем откройте файл Global. asax. Добавьте следующий код в метод **\_запуска приложения** :

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
