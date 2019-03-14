---
uid: signalr/overview/performance/signalr-performance
title: Производительность SignalR | Документация Майкрософт
author: bradygaster
description: Производительность SignalR
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 3326c2e600854fc7a4435d96c45b04a6188d3937
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046741"
---
<a name="signalr-performance"></a>Производительность SignalR
====================
по [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом разделе описывается, как спроектировать архитектуру, измерения и повышения производительности в приложении SignalR.
>
> ## <a name="software-versions-used-in-this-topic"></a>Версии программного обеспечения, используемого в этом разделе
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR версии 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Предыдущие версии этого раздела
>
> Сведения о более ранних версий SignalR, см. в разделе [более старых версий SignalR](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Вопросы и комментарии
>
> Оставьте свои отзывы на том, как вам понравилось, и этот учебник и что можно улучшить в комментариях в нижней части страницы. Если у вас есть вопросы, которые не имеют отношения к руководству, их можно разместить [форум по ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) или [StackOverflow.com](http://stackoverflow.com/).


Недавней презентации на производительность SignalR и масштабирования, см. в разделе [масштабирование в Интернете в реальном времени с помощью ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).

В этом разделе содержатся следующие подразделы.

- [Рекомендации по проектированию](#design)
- [Помощник по настройке производительность сервера SignalR](#tuning)
- [Устранение неполадок производительности](#troubleshooting)
- [Использование счетчиков производительности SignalR](#perfcounters)
- [Использование других счетчиков производительности](#othercounters)
- [Другие ресурсы](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>Рекомендации по проектированию

В этом разделе описаны шаблоны, которые можно реализовать при разработке приложения SignalR, чтобы убедиться, что не выполняется ухудшить производительность путем создания лишний сетевой трафик.

### <a name="throttling-message-frequency"></a>Частота запросов сообщений

Даже в приложении, отправки сообщений с высокой частотой (например, приложение игры в реальном времени) большинство приложений не нужно отправлять несколько сообщений в секунду. Чтобы уменьшить объем трафика, создаваемую каждый клиент, цикл обработки сообщений можно реализовать, очереди и отправки сообщений не более часто фиксированной ставке (то есть до определенного числа сообщений будут отправляться каждую секунду, при наличии сообщений в это время в Интервал отправки). Пример приложения, который регулирует поток сообщений, определенных скорость (от сервера и клиента), см. в разделе [высокой частотой в реальном времени с SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).

### <a name="reducing-message-size"></a>Уменьшая размер сообщения

Можно уменьшить размер сообщения SignalR, уменьшив размер сериализованных объектов. В серверном коде, если вы отправляете объект, содержащий свойства, которые не должны передаваться, предотвратить эти свойства сериализацию с помощью `JsonIgnore` атрибута. Имена свойств, также сохраняются в сообщение; имена свойств может быть сокращено с помощью `JsonProperty` атрибута. В следующем образце кода показано, как исключить свойство отправку клиенту и сокращение имена свойств:

**Код сервера .NET, который демонстрирует атрибут JsonIgnore, чтобы исключить данные отправку клиенту и атрибут JsonProperty, чтобы уменьшить размер сообщения**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

Чтобы сохранить удобочитаемость / сопровождения в клиентском коде имена сокращенное свойство может быть пересопоставленный в понятном имена после получения сообщения. В следующем образце кода демонстрируется один из возможных способов повторного сопоставления названия для больше из них, путем определения контракта сообщения (сопоставление) и с помощью `reMap` функция, применяемая к классу оптимизированного сообщений контракта:

**Код JavaScript на стороне клиента, который указывает, что используется сокращение имен свойств понятное именами**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

Имена может быть сокращено в сообщениях от клиента к серверу, используя тот же метод.

Используемый объем памяти (то есть, объем памяти, используемой для сообщения) сообщения объект также может повысить производительность. Например если полный спектр `int` не требуется, `short` или `byte` взамен можно использовать.

Так как сообщения хранятся в канале сообщений в памяти сервера, уменьшение размера сообщения также могут устранить проблемы памяти сервера.

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>Помощник по настройке производительность сервера SignalR

Следующие параметры конфигурации можно использовать для настройки сервера для повышения производительности в приложении SignalR. Общие сведения о том, как повысить производительность в приложении ASP.NET, см. в разделе [повышение производительности ASP.NET](https://msdn.microsoft.com/library/ff647787.aspx).

**Параметры конфигурации SignalR**

- **DefaultMessageBufferSize**: По умолчанию SignalR сохраняет 1000 сообщений в памяти на каждый центр на соединение. Если используются большие сообщения, это может создать проблемы с памятью, которые можно устранить, уменьшая это значение. Этот параметр можно задать в `Application_Start` обработчик событий в приложении ASP.NET или в `Configuration` метод класса запуска OWIN в резидентного приложения. В следующем образце показано, как уменьшить это значение, чтобы сократить использование памяти приложения, чтобы сократить объем используемой памяти сервера:

    **.NET серверного кода в файле Startup.cs уменьшение размера буфера сообщения по умолчанию**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**Параметры конфигурации IIS**

- **Максимум одновременных запросов в приложение**: Увеличение количества одновременных IIS запросов будет увеличить ресурсы сервера, доступных для обслуживания запросов. Значение по умолчанию — 5000; Чтобы увеличить этот параметр, выполните следующие команды в командной строке с повышенными правами:

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**: Это максимальное число запросов, что Http.sys помещает в очередь для пула приложений. Когда очередь заполнена, новые запросы ответ 503 «Служба недоступна». Значение по умолчанию — 1000.

    Сокращение длины очереди для рабочего процесса в пуле приложений, размещение приложения будет экономии ресурсов памяти. Дополнительные сведения см. в разделе [управление, помощник по настройке и Настройка групп приложений](https://technet.microsoft.com/library/cc745955.aspx).

**Параметры конфигурации ASP.NET**

Этот раздел содержит параметры конфигурации, которые могут устанавливаться в `aspnet.config` файл. Этот файл находится в одном из двух расположений, в зависимости от платформы:

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

Следующие параметры ASP.NET, которые могут повысить производительность SignalR.

- **Максимальное число параллельных запросов на один ЦП**: Увеличение значения этого параметра может устранить узкие места производительности. Чтобы увеличить этот параметр, добавьте следующий параметр конфигурации в `aspnet.config` файла:

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **Предел очереди запросов**: Если общее число подключений превышает `maxConcurrentRequestsPerCPU` параметр ASP.NET начнется регулирование запросов с использованием очереди. Чтобы увеличить размер очереди, можно увеличить `requestQueueLimit` параметр. Чтобы сделать это, добавьте следующий параметр конфигурации в `processModel` узел в `config/machine.config` (а не `aspnet.config`):

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>Устранение неполадок производительности

В этом разделе описываются способы поиска узких мест производительности в приложении.

### <a name="verifying-that-websocket-is-being-used"></a>Проверка того, что используется WebSocket

Хотя SignalR можно использовать различные транспорты для обмена данными между клиентом и сервером, WebSocket предлагает это значительно быстрее и следует использовать, если клиент и сервер поддерживают его. Чтобы определить, если клиент и сервер соответствия требованиям к WebSocket, см. в разделе [транспорта и в случае ошибки](../getting-started/introduction-to-signalr.md#transports). Чтобы определить, какой транспорт используется в приложении, можно использовать средства разработчика браузера и изучить журналы, чтобы узнать, какой транспорт используется для подключения. Сведения об использовании средства разработки браузера в Internet Explorer и Chrome, см. в разделе [транспорта и в случае ошибки](../getting-started/introduction-to-signalr.md#transports).

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>Использование счетчиков производительности SignalR

В этом разделе описывается включение и использование счетчиков производительности SignalR, найден в `Microsoft.AspNet.SignalR.Utils` пакета.

### <a name="installing-signalrexe"></a>Установка signalr.exe

Счетчики производительности можно добавить на сервер, с помощью служебной программы, называется SignalR.exe. Чтобы установить эту программу, выполните следующие действия.

1. В Visual Studio выберите **средства** > **диспетчер пакетов NuGet** > **управление пакетами NuGet для решения**
2. Поиск **signalr.utils**и выберите команду установить.

    ![](signalr-performance/_static/image1.png)
3. Примите лицензионное соглашение для установки пакета.
4. Будет установлен SignalR.exe `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.

### <a name="installing-performance-counters-with-signalrexe"></a>Установка счетчиков производительности с SignalR.exe

Чтобы установить счетчиков производительности SignalR, запустите SignalR.exe в командную строку со следующим параметром:

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

Чтобы удалить счетчики производительности SignalR, выполните SignalR.exe в командную строку со следующим параметром:

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>Счетчики производительности SignalR

Служебные программы пакет устанавливает следующие счетчики производительности. Счетчики «Всего» измеряет число событий с момента последнего пул приложений или сервере перезапуска.

**Метрик подключения**

Следующие метрики измерения возникающих событий время существования подключения. Дополнительные сведения см. в разделе [понимание и обработка событий времени существования подключений](../guide-to-the-api/handling-connection-lifetime-events.md).

- **Подключений**
- **Подключения повторно присоединена**
- **Подключения к отключении**
- **Текущих подключений**

**Метрики использования**

Следующие метрики измерения сообщение трафик, создаваемый SignalR.

- **Всего получено сообщение соединения**
- **Всего отправлено сообщение соединения**
- **Подключение сообщений, полученных в секунду**
- **Подключения сообщений, отправляемых в секунду**

**Метрики шины сообщений**

Следующие метрики измерения трафика через внутренний сообщений SignalR, очереди, в которой размещаются всех входящих и исходящих сообщений SignalR. Сообщение **опубликовано** при его отправке или вещания. Объект **подписчика** в данном контексте — это подписка на канал сообщений; это должно быть равно количество клиентов, а также сам сервер. **Выделенной рабочей роли** — это компонент, который отправляет данные в активных соединений; **занятых рабочих** — это приложения, активно отправляет сообщение.

- **Канал сообщений полученных всего сообщений**
- **Канал сообщений сообщений, полученных в секунду**
- **Общее число опубликованных Message шины сообщений**
- **Канал сообщений сообщения, опубликованные в секунду**
- **Текущий подписчиков шины сообщений**
- **Общее число подписчиков шины сообщений**
- **Подписчики шины сообщений в секунду**
- **Канал сообщений, выделенных рабочих ролей**
- **Занятых рабочих процессов для шины сообщений**
- **Текущий разделы шины сообщений**

**Погрешность**

Следующие метрики измерения ошибки, создаваемые трафиком сообщений SignalR. **Разрешения центра** ошибки возникают, когда концентратор или метода концентратора, не может быть разрешена. **Вызов концентратора** ошибки, исключения, возникшие во время вызова метода концентратора. **Транспорт** ошибки — ошибки подключения, создается во время HTTP-запроса или ответа.

- **Ошибки: Общее число всех**
- **Ошибки: Все в секунду**
- **Ошибки: Общее разрешение концентратора**
- **Ошибки: Разрешение концентратора в секунду**
- **Ошибки: Общее число вызовов концентратора**
- **Ошибки: Центр вызовов/сек**
- **Ошибки: Всего транспорта**
- **Ошибки: Транспорт за секунду**

<a id="scaleout_metrics"></a>

**Метрики горизонтального масштабирования**

Следующие метрики измерения трафика и ошибки, создаваемые поставщиком горизонтального масштабирования. Объект **Stream** в этом контексте в единицу масштабирования, используемый поставщиком горизонтального масштабирования; это таблицы, если используется SQL Server, раздел, если используется служебной шины и подписки, если используется Redis. Каждый поток гарантирует упорядоченную операций чтения и записи; один поток является потенциальных узких мест масштабирования, поэтому можно увеличить количество потоков с целью сокращения появления узкого места. Если используются несколько потоков, SignalR автоматически распространять сообщения (сегментов) для этих потоков способом, который гарантирует, что сообщения, отправленные из любого соединения расположены в порядке.

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) настройку перемещения по элементам, длина очереди отправки горизонтального масштабирования, обслуживается SignalR. Установите в значение больше 0 будет помещать все сообщения в очереди отправки, который должны отправляться по одному настроенных объединительной платы сообщений. Если размер очереди превышает настроенный длина, последующие вызовы для отправки будет завершаться сбоем с [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) пока число сообщений в очереди меньше, чем задано параметром еще раз. Постановка в очередь по умолчанию отключена, так как реализованные соединительных панелях обычно имеют свои собственные очереди или управления потоком на месте. В случае SQL Server организация пулов соединений эффективно ограничивает количество отправляет, происходящего в любой момент времени.

По умолчанию используется только один поток для SQL Server и Redis, пять потоков используются для служебной шины и их постановку в очередь отключена, но эти параметры можно изменить с помощью конфигурации на сервере SQL и служебной шины:

**Код сервера .NET для настройки таблицы count или длины очереди SQL Server объединительной платы**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**Код сервера .NET для настройки раздела count или длины очереди служебной шины объединительной платы**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

Объект **буферизация** поток — это приложения, перешла в состояние faulted, когда поток находится в состоянии сбоя, все сообщения, отправляемые на объединительную плату завершится неудачей, немедленно в том случае, пока поток больше не произошла ошибка. **Длина очереди отправки** — количество сообщений, которые были опубликованы, но еще не отправлены.

- **Канал сообщений горизонтального масштабирования сообщений, полученных в секунду**
- **Общее число потоков горизонтального масштабирования**
- **Горизонтального масштабирования выполняет потоковую передачу открытым**
- **Буферизация потоков горизонтального масштабирования**
- **Всего ошибок горизонтального масштабирования**
- **Ошибок горизонтального масштабирования в секунду**
- **Длину очереди отправленных сообщений горизонтального масштабирования**

Дополнительные сведения об этих счетчиков, которые измерения, см. в разделе [масштабирование SignalR с помощью служебной шины Azure](scaleout-with-windows-azure-service-bus.md).

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>Использование других счетчиков производительности

Следующие счетчики производительности также может быть полезными для наблюдения за производительностью приложения.

**Память**

- Память .NET CLR\\байт во всех кучах (для w3wp)

**ASP.NET**

- ASP.NET\Requests Current
- ASP.NET\Queued
- ASP.NET\Rejected

**ЦП**

- Information\Processor загруженности процессора

**TCP/IP**

- TCPv6/подключений
- TCPv4/подключений

**Веб-службы**

- Веб-служба\текущих подключений
- Веб-Service\Maximum подключений

**Работа с потоками**

- .NET блокировки и потоки CLR\\текущих логических потоков
- .NET блокировки и потоки CLR\\число текущих физических потоков

<a id="otherresources"></a>

## <a name="other-resources"></a>Другие ресурсы

Дополнительные сведения по мониторингу и настройке производительности ASP.NET см. в разделах:

- [Общие сведения о производительности ASP.NET](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [Использование потоков ASP.NET в IIS 7.5, IIS 7.0 и IIS 6.0](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;пул приложений&gt; элемент (веб-параметры)](https://msdn.microsoft.com/library/dd560842.aspx)