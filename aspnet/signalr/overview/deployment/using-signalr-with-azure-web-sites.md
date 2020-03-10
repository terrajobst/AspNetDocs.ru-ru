---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Использование SignalR с веб-приложениями в службе приложений Azure | Документация Майкрософт
author: bradygaster
description: В этом документе описывается настройка приложения SignalR, которое выполняется на Microsoft Azure. Версии программного обеспечения, используемые в учебнике Visual Studio 2013 или обратитесь...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450186"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a>Использование SignalR с веб-приложениями в службе приложений Azure

по [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом документе описывается настройка приложения SignalR, которое выполняется на Microsoft Azure.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) или Visual Studio 2012
> - .NET 4.5
> - SignalR версии 2
> - Пакет Azure SDK 2,3 для Visual Studio 2013 или 2012
>
>
>
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
>
> Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы. Если у вас есть вопросы, которые не связаны непосредственно с этим руководством, вы можете разместить их на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/)или на [форумах Microsoft Azure](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).

## <a name="table-of-contents"></a>Оглавление

- [Введение](#introduction)
- [Развертывание веб-приложения SignalR в службе приложений Azure](#deploying)
- [Включение WebSocket в службе приложений Azure](#websocket)
- [Использование объединительной платы кэша Redis для Azure](#backplane)
- [Следующие шаги](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>Введение

ASP.NET SignalR можно использовать для создания нового уровня интерактивности между серверами, а также веб-клиентами или клиентами .NET. При размещении в Azure приложения SignalR могут воспользоваться преимуществами высокодоступной, масштабируемой и высокопроизводительной среды, работающей в облаке.

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>Развертывание веб-приложения SignalR в службе приложений Azure

SignalR не добавляет каких-либо особых осложнений к развертыванию приложения в Azure и развертывании на локальном сервере. Приложение, использующее SignalR, может быть размещено в Azure без каких-либо изменений в конфигурации или других параметрах (хотя для поддержки WebSocket см. раздел [Включение WebSockets в службе приложений Azure](#websocket) ниже). В этом руководстве вы развернете приложение, созданное в [руководстве по начало работы](../getting-started/tutorial-getting-started-with-signalr.md) , в Azure.

**Предварительные требования**

- Visual Studio 2013. Если у вас нет Visual Studio, Visual Studio 2013 Express for Web включен в установку пакета SDK для Azure.
- [Пакет Azure sdk 2,3 для Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) или [Azure SDK 2,3 для Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).
- Для работы с этим учебником вам потребуется подписка Azure. Вы можете [активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)или [зарегистрироваться для получения пробной подписки](https://azure.microsoft.com/pricing/free-trial/).

### <a name="deploying-a-signalr-web-app-to-azure"></a>Развертывание веб-приложения SignalR в Azure

1. Выполните инструкции [Начало работы руководстве](../getting-started/tutorial-getting-started-with-signalr.md)или скачайте готовый проект из [коллекции кода](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).
2. В Visual Studio выберите **Сборка**и **опубликуйте SignalR Chat**.
3. В диалоговом окне "опубликовать веб-сайт" выберите "веб-сайты Windows Azure".

    ![Выбор веб-сайтов Azure](using-signalr-with-azure-web-sites/_static/image1.png)
4. Если вы не вошли в учетная запись Майкрософт, щелкните **войти...** в диалоговом окне "Выбор существующего веб-сайта" и выполните вход.

    ![Выберите существующий веб-сайт](using-signalr-with-azure-web-sites/_static/image2.png)    ![Вход в Azure](using-signalr-with-azure-web-sites/_static/image3.png)
5. В диалоговом окне "Выбор существующего веб-сайта" нажмите кнопку **создать**.

    ![Новый веб-сайт](using-signalr-with-azure-web-sites/_static/image4.png)
6. В диалоговом окне "Создание сайта в Windows Azure" введите уникальное имя приложения. Выберите ближайший к вам регион в раскрывающемся списке регион. Нажмите кнопку **Создать**.

    ![Создание сайта в Azure](using-signalr-with-azure-web-sites/_static/image5.png)
7. В диалоговом окне "Публикация веб-сайта" нажмите кнопку **опубликовать**.

    ![Опубликовать сайт](using-signalr-with-azure-web-sites/_static/image6.png)
8. Когда приложение завершит публикацию, приложение для разговора с SignalR, размещенное в веб-приложениях службы приложений Azure, откроется в браузере.

    ![Открытие сайта в браузере](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>Включение WebSocket в веб-приложениях службы приложений Azure

Для использования в приложении SignalR необходимо явно включить соединения WebSockets в веб-приложении; в противном случае будут использоваться другие протоколы (Дополнительные сведения см. в разделе [транспорты и резервные](../getting-started/introduction-to-signalr.md#transports) ).

Чтобы использовать WebSockets в веб-приложениях службы приложений Azure, включите его в разделе конфигурации веб-приложения. Для этого откройте веб-приложение в [портал управления Azure](https://manage.windowsazure.com/)и выберите настроить.

![Вкладка "Настройка"](using-signalr-with-azure-web-sites/_static/image8.png)

В верхней части страницы Конфигурация убедитесь, что для веб-приложения используется .NET 4,5.

![Параметр .NET Framework версии 4,5](using-signalr-with-azure-web-sites/_static/image9.png)

На странице Конфигурация в параметре **WebSockets** выберите **вкл**.

![Параметр WebSockets: вкл.](using-signalr-with-azure-web-sites/_static/image10.png)

В нижней части страницы Конфигурация нажмите кнопку **сохранить** , чтобы сохранить изменения.

![Сохранить параметры](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>Использование объединительной платы кэша Redis для Azure

Если для веб-приложения используется несколько экземпляров, и пользователям этих экземпляров необходимо взаимодействовать друг с другом (например, сообщения разговора, созданные в одном экземпляре, могут достигать пользователей, подключенных к другим экземплярам), в приложении должна быть реализована [Объединительная плата кэша Redis для Azure](../performance/scaleout-with-redis.md) .

<a id="nextsteps"></a>
## <a name="next-steps"></a>Next Steps

Дополнительные сведения о веб-приложениях в службе приложений Azure см. в статье [Обзор веб-приложений](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).
