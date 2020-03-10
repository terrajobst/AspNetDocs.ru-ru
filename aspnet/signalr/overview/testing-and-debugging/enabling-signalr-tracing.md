---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: Включение трассировки SignalR | Документация Майкрософт
author: bradygaster
description: В этом документе описано, как включить и настроить трассировку для серверов и клиентов SignalR. Трассировка позволяет просматривать диагностические сведения о событиях...
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467442"
---
# <a name="enabling-signalr-tracing"></a>Включение трассировки SignalR

от [Tom фитзмаккен](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом документе описано, как включить и настроить трассировку для серверов и клиентов SignalR. Трассировка позволяет просматривать диагностические сведения о событиях в приложении SignalR.
>
> Этот раздел изначально был написан с помощью Патрик Флетчера.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET Framework 4.5
> - SignalR версии 2
>
>
>
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
>
> Оставьте отзыв о том, как вы понравится вам в этом учебнике, и что можно улучшить в комментариях в нижней части страницы. Если у вас есть вопросы, не связанные непосредственно с этим руководством, их можно опубликовать на [форуме ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).

Когда трассировка включена, приложение SignalR создает записи журнала для событий. События можно регистрировать как из клиента, так и с сервера. Трассировка на сервере регистрирует соединение, масштабируемый поставщик и события шины сообщений. Трассировка на клиенте регистрирует события соединения. В SignalR 2,1 и более поздних версиях трассировка на клиенте записывает в журнал полное содержимое сообщений о вызовах концентратора.

## <a name="contents"></a>Содержимое

- [Включение трассировки на сервере](#server)

    - [Ведение журнала событий сервера в текстовые файлы](#server_text)
    - [Ведение журнала событий сервера в журнале событий](#server_eventlog)
- [Включение трассировки в клиенте .NET (классическое приложение для Windows)](#net_client)

    - [Запись событий клиента настольных систем в консоль](#desktop_console)
    - [Запись событий клиента рабочего стола в текстовый файл](#desktop_text)
- [Включение трассировки в клиентах Windows Phone 8](#phone)

    - [Ведение журнала Windows Phone событий клиента в пользовательском интерфейсе](#phone_ui)
    - [Запись событий клиента Windows Phone в консоль отладки](#phone_debug)
- [Включение трассировки в клиенте JavaScript](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>Включение трассировки на сервере

Трассировка включается на сервере в файле конфигурации приложения (файл App. config или Web. config в зависимости от типа проекта). Укажите категории событий, которые необходимо заносить в журнал. В файле конфигурации также указывается, следует ли записывать события в текстовый файл, в журнал событий Windows или в пользовательский журнал, используя реализацию [прослушивателя TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).

К категориям событий сервера относятся следующие виды сообщений:

| Источник | Сообщения |
| --- | --- |
| SignalR. Склмессажебус | Установка поставщика масштабирования шины сообщений SQL, события базы данных, ошибки и время ожидания |
| SignalR.ServiceBusMessageBus | Создание раздела поставщика масштабирования служебной шины и события подписки, ошибок и сообщений |
| SignalR. Редисмессажебус | Redis, отключение и события ошибок для поставщика масштабирования. |
| SignalR. Скалеаутмессажебус | Масштабирование событий обмена сообщениями |
| SignalR. транспорт. Вебсоккеттранспорт | Транспортное соединение WebSocket, отключение, Обмен сообщениями и события ошибок |
| SignalR. транспорт. Серверсентевентстранспорт | Серверсентевентс транспортное соединение, отключение, Обмен сообщениями и события ошибок |
| SignalR. транспорт. Фореверфраметранспорт | Фореверфраме транспортное соединение, отключение, Обмен сообщениями и события ошибок |
| SignalR.Transports.LongPollingTransport | Лонгполлинг транспортное соединение, отключение, Обмен сообщениями и события ошибок |
| SignalR.Transports.TransportHeartBeat | Транспортные подключения, отключение и события KeepAlive |
| SignalR. Рефлектедхубдескрипторпровидер | События обнаружения концентратора |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>Ведение журнала событий сервера в текстовые файлы

В следующем коде показано, как включить трассировку для каждой категории события. Этот пример настраивает приложение для записи событий в текстовые файлы.

**Код XML-сервера для включения трассировки**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

В приведенном выше коде запись `SignalRSwitch` указывает значение [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) , используемое для событий, отправляемых в указанный журнал. В этом случае для него задается значение `Verbose` что означает, что все сообщения отладки и трассировки записываются в журнал.

Следующие выходные данные показывают записи из файла `transports.log.txt` для приложения, в котором используется указанный выше файл конфигурации. В нем отображается новое подключение, удаленное подключение и события пульса передачи.

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>Ведение журнала событий сервера в журнале событий

Чтобы регистрировать события в журнале событий, а не в текстовом файле, измените значения записей в узле `sharedListeners`. В следующем коде показано, как регистрировать события сервера в журнале событий:

**Код XML-сервера для ведения журнала событий в журнале событий**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

События регистрируются в журнале приложений и доступны через Просмотр событий, как показано ниже:

![Просмотр событий отображения журналов SignalR](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> При использовании журнала событий установите для параметра **TraceLevel** значение **Error** , чтобы поддерживать Управление числом сообщений.

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>Включение трассировки в клиенте .NET (классическое приложение для Windows)

Клиент .NET может регистрировать события в консоли, текстовом файле или пользовательском журнале с помощью реализации [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).

Чтобы включить ведение журнала в клиенте .NET, задайте для свойства `TraceLevel` соединения значение [трацелевелс](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) , а свойству `TraceWriter` — допустимый экземпляр [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) .

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>Запись событий клиента настольных систем в консоль

В следующем C# коде показано, как регистрировать события в клиенте .NET на консоли.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>Запись событий клиента рабочего стола в текстовый файл

В следующем C# коде показано, как регистрировать события в клиенте .NET в текстовом файле.

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

Следующие выходные данные показывают записи из файла `ClientLog.txt` для приложения, в котором используется указанный выше файл конфигурации. В нем отображается клиент, подключающийся к серверу, а в концентраторе вызывается клиентский метод с именем `addMessage`:

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>Включение трассировки в клиентах Windows Phone 8

Приложения SignalR для Windows Phoneных приложений используют один и тот же клиент .NET в качестве классических приложений, но [консоль. out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) и запись в файл с помощью [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) недоступны. Вместо этого необходимо создать пользовательскую реализацию [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) для трассировки.

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>Ведение журнала Windows Phone событий клиента в пользовательском интерфейсе

[База кода SignalR](https://github.com/SignalR/SignalR/archive/master.zip) содержит Windows Phone пример, который записывает выходные данные трассировки в [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) с помощью пользовательской реализации [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) , именуемой `TextBlockWriter`. Этот класс можно найти в проекте **Samples/Microsoft. AspNet. SignalR. Client. WP8. Samples** . При создании экземпляра `TextBlockWriter`передайте текущий [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)и [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) , где будет создан [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) , используемый для вывода трассировки:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

Затем выходные данные трассировки будут записаны в новый [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) , созданный в переданном [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) .

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>Запись событий клиента Windows Phone в консоль отладки

Чтобы отправить выходные данные в консоль отладки, а не в пользовательский интерфейс, создайте реализацию [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) , которая выполняет запись в окно отладки, и назначьте ее свойству [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) соединения:

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

Данные трассировки будут записаны в окно отладки в Visual Studio:

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>Включение трассировки в клиенте JavaScript

Чтобы включить ведение журнала на стороне клиента для соединения, задайте свойство `logging` объекта соединения перед вызовом метода `start` для установления соединения.

**Клиентский код JavaScript для включения трассировки в консоль браузера (с созданным прокси-сервером)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**Клиентский код JavaScript для включения трассировки в консоль браузера (без созданного прокси-сервера)**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

Когда трассировка включена, клиент JavaScript регистрирует события в консоли браузера. Сведения о доступе к консоли браузера см. в разделе [мониторинг транспортов](../getting-started/introduction-to-signalr.md#MonitoringTransports).

На следующем снимке экрана показан клиент на JavaScript SignalR с включенной трассировкой. В консоли браузера отображаются события вызова подключения и концентратора:

![События трассировки SignalR в консоли браузера](enabling-signalr-tracing/_static/image4.png)
