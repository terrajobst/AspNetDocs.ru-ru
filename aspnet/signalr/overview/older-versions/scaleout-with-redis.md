---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Масштабирование SignalR с помощью Redis (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431208"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a>Масштабирование SignalR с помощью Redis (SignalR 1.x)

по [Майк Уоссон](https://github.com/MikeWasson), [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

В этом руководстве вы будете использовать [Redis](http://redis.io/) для распространения сообщений в приложении SignalR, которое развернуто на двух отдельных экземплярах IIS.

Redis — это хранилище "ключ — значение" в памяти. Она также поддерживает систему обмена сообщениями с моделью публикации и подписки. Для пересылки сообщений на другие серверы в объединительной плате Redis SignalR используется функция Pub/Re-in.

![](scaleout-with-redis/_static/image1.png)

В рамках этого руководства вы будете использовать три сервера:

- Два сервера под Windows, которые будут использоваться для развертывания приложения SignalR.
- Один сервер под управлением Linux, который будет использоваться для запуска Redis. Для снимков экрана в этом учебнике я использовал Ubuntu 12,04 TLS.

Если у вас нет трех физических серверов, можно создать виртуальные машины в Hyper-V. Другой вариант — создать виртуальные машины в Azure.

Хотя в этом учебнике используется официальная реализация Redis, в MSOpenTech также есть [порт Windows Redis](https://github.com/MSOpenTech/redis) . Установка и настройка различаются, но в противном случае шаги одинаковы.

> [!NOTE] 
> 
> Масштабирование SignalR с помощью Redis не поддерживает кластеры Redis.

## <a name="overview"></a>Обзор

Прежде чем приступить к работе с подробным руководством, ознакомьтесь с кратким обзором того, что вы сделаете.

1. Установите Redis и запустите сервер Redis.
2. Добавьте следующие пакеты NuGet в приложение: 

    - [Microsoft. AspNet. SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. AspNet. SignalR. Redis](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. Создание приложения SignalR.
4. Добавьте следующий код в Global. asax для настройки объединительной платы: 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Ubuntu на Hyper-V

С помощью Windows Hyper-V вы можете легко создать виртуальную машину Ubuntu на Windows Server.

Скачайте ISO-образ Ubuntu с [http://www.ubuntu.com](http://www.ubuntu.com/).

В Hyper-V добавьте новую виртуальную машину. На шаге **Подключить виртуальный жесткий диск** выберите **создать виртуальный жесткий диск**.

![](scaleout-with-redis/_static/image2.png)

На шаге **Параметры установки** выберите **файл образа (. ISO)** , нажмите кнопку **Обзор**и перейдите к ISO-образ установки Ubuntu.

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>Установка Redis

Выполните действия, описанные в [http://redis.io/download](http://redis.io/download) , чтобы скачать и создать Redis.

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

Это приведет к сборке двоичных файлов Redis в каталоге `src`.

По умолчанию Redis не требует пароля. Чтобы задать пароль, измените файл `redis.conf`, который находится в корневом каталоге исходного кода. (Создайте резервную копию файла, прежде чем изменять его!) Добавьте следующую директиву в `redis.conf`:

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

Теперь запустите сервер Redis:

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

Откройте порт 6379. это порт по умолчанию, который прослушивается Redis. (Номер порта можно изменить в файле конфигурации.)

## <a name="create-the-signalr-application"></a>Создание приложения SignalR

Создайте приложение SignalR, следуя одному из следующих учебников:

- [начало работы с SignalR](../getting-started/tutorial-getting-started-with-signalr.md)
- [начало работы с SignalR и MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)

Далее мы изменим приложение разговора для поддержки масштабирования с помощью Redis. Сначала добавьте в проект пакет NuGet SignalR. Redis. В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

Затем откройте файл Global. asax. Добавьте следующий код в метод **\_запуска приложения** :

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "Server" — имя сервера, на котором работает Redis.
- *порт* — номер порта.
- Password — это пароль, определенный в файле Redis. conf.
- AppName — любая строка. SignalR создает канал Pub/Redis с таким именем.

Пример:

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>Развертывание и запуск приложения

Подготовьте экземпляры Windows Server к развертыванию приложения SignalR.

Добавьте роль IIS. Включите функции разработки приложений, включая протокол WebSocket.

![](scaleout-with-redis/_static/image5.png)

Также включите службу управления (указанную в разделе "средства управления").

![](scaleout-with-redis/_static/image6.png)

**Установите веб-развертывание 3,0.** При запуске диспетчера IIS будет предложено установить веб-платформу Майкрософт, или вы можете [скачать установщик](https://go.microsoft.com/fwlink/?LinkId=255386). В установщике платформы найдите веб-развертывание и установите веб-развертывание 3,0.

![](scaleout-with-redis/_static/image7.png)

Убедитесь, что служба веб-управления запущена. В противном случае запустите службу. (Если служба веб-управления не отображается в списке служб Windows, убедитесь, что служба управления установлена при добавлении роли IIS.)

По умолчанию служба веб-управления прослушивает порт TCP 8172. В брандмауэре Windows создайте новое правило для входящего трафика, разрешающее TCP-трафик через порт 8172. Дополнительные сведения см. в разделе [Настройка правил брандмауэра](https://technet.microsoft.com/library/dd448559(WS.10).aspx). (Если вы размещаете виртуальные машины в Azure, это можно сделать непосредственно в портал Azure. См. раздел [Настройка конечных точек для виртуальной машины](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)

Теперь все готово для развертывания проекта Visual Studio с компьютера разработки на сервере. В обозреватель решений щелкните решение правой кнопкой мыши и выберите пункт **опубликовать**.

Более подробную документацию по веб-развертыванию см. в разделе [веб-развертывание Map Web для Visual Studio и ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).

При развертывании приложения на двух серверах можно открыть каждый экземпляр в отдельном окне браузера и увидеть, что каждый из них получает сообщения SignalR от другого. (Конечно, в рабочей среде два сервера будут находиться за подсистемой балансировки нагрузки.)

![](scaleout-with-redis/_static/image8.png)

Если вы хотите просмотреть сообщения, отправленные в Redis, можно использовать клиент **Redis-CLI** , который устанавливается вместе с Redis.

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
