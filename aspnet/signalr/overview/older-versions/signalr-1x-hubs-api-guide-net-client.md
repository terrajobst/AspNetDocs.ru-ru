---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: Путеводитель по API концентраторов SignalR ASP.NET — клиент .NET (SignalR 1. x) | Документация Майкрософт
author: bradygaster
description: В этом документе приводятся общие сведения об использовании API концентраторов для SignalR версии 2 в клиентах .NET, таких как Магазин Windows (WinRT), WPF, Silverlight и недостатки...
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 2b22b53c405a865f91b04e677f60b82dd46dbf9b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505974"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a>Путеводитель по API концентраторов SignalR ASP.NET — клиент .NET (SignalR 1. x)

[Патрик Флетчера](https://github.com/pfletcher), [Tom Dykstra)](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом документе содержатся общие сведения об использовании API концентраторов для SignalR версии 2 в клиентах .NET, таких как Магазин Windows (WinRT), WPF, Silverlight и консольные приложения.
> 
> API концентраторов SignalR позволяет выполнять удаленные вызовы процедур (RPC) с сервера на подключенные клиенты и с клиентов на сервер. В серверном коде определяются методы, которые могут вызываться клиентами, и вызываются методы, которые выполняются на клиенте. В клиентском коде определяются методы, которые могут быть вызваны с сервера, а также вызываются методы, которые выполняются на сервере. Этот механизм отвечает за все клиентские коммуникации.
> 
> SignalR также предлагает интерфейс API более низкого уровня, называемый постоянными подключениями. Общие сведения о SignalR, концентраторах и постоянных подключениях, а также руководство, в котором показано, как создать полноценное приложение SignalR, см. в разделе [SignalR-начало работы](../getting-started/index.md).

## <a name="overview"></a>Обзор

Этот документ содержит следующие разделы.

- [Установка клиента](#clientsetup)
- [Как установить соединение](#establishconnection)

    - [Междоменные соединения от клиентов Silverlight](#slcrossdomain)
- [Настройка подключения](#configureconnection)

    - [Установка максимального числа одновременных подключений в клиентах WPF](#maxconnections)
    - [Указание параметров строки запроса](#querystring)
    - [Как указать метод перевозки](#transport)
    - [Как указать заголовки HTTP](#httpheaders)
    - [Как указать сертификаты клиента](#clientcertificate)
- [Создание прокси-сервера концентратора](#proxy)
- [Определение методов на клиенте, который может вызывать сервер](#callclient)

    - [Методы без параметров](#clientmethodswithoutparms)
    - [Методы с параметрами, указание типов параметров](#clientmethodswithparmtypes)
    - [Методы с параметрами, указание динамических объектов для параметров](#clientmethodswithdynamparms)
    - [Удаление обработчика](#removehandler)
- [Вызов методов сервера из клиента](#callserver)
- [Как работать с событиями времени жизни соединения](#connectionlifetime)
- [Как обрабатывались ошибки](#handleerrors)
- [Как включить ведение журнала на стороне клиента](#logging)
- [Примеры кода приложений WPF, Silverlight и консольного приложения для клиентских методов, которые может вызывать сервер](#wpfsl)

Примеры клиентских проектов .NET см. в следующих ресурсах:

- [Густаво-Армента/SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) на GitHub.com (WinRT, Silverlight, примеры консольного приложения).
- [Дамианедвардс/SignalR-мовешапедемо/мовешапе. Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) на GitHub.com (пример с WPF).
- [SignalR/Microsoft. AspNet. SignalR. Client. Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (пример консольного приложения).

Документацию по программированию клиентов сервера или JavaScript см. в следующих ресурсах:

- [Путеводитель по API концентраторов SignalR — сервер](../guide-to-the-api/hubs-api-guide-server.md)
- [Путеводитель по API концентраторов SignalR — клиент JavaScript](../guide-to-the-api/hubs-api-guide-javascript-client.md)

Ссылки на справочные статьи по API относятся к версии .NET 4,5 API. Если вы используете .NET 4, см. [статьи с описанием API для .NET 4](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).

<a id="clientsetup"></a>

## <a name="client-setup"></a>Настройка клиента

Установите пакет NuGet [Microsoft. ASPNET. SignalR. Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) (не пакет [Microsoft. ASPNET. SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) ). Этот пакет поддерживает клиентские приложения WinRT, Silverlight, WPF, консольное приложение и Windows Phone для .NET 4 и .NET 4,5.

Если версия SignalR, установленная на клиенте, отличается от версии на сервере, то SignalR часто может адаптироваться к разнице. Например, когда выдается SignalR версии 2,0 и устанавливается на сервере, сервер будет поддерживать клиенты, на которых установлен выпуск 1.1. x, а также клиенты, на которых установлено 2,0. Если разница между версией на сервере и версией на клиенте слишком велика, SignalR вызывает исключение `InvalidOperationException`, когда клиент пытается установить соединение. Сообщение об ошибке: "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>Как установить соединение

Прежде чем установить соединение, необходимо создать объект `HubConnection` и создать прокси-сервер. Чтобы установить соединение, вызовите метод `Start` для объекта `HubConnection`.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> Для клиентов JavaScript необходимо зарегистрировать по крайней мере один обработчик событий перед вызовом метода `Start` для установления соединения. Это не является обязательным для клиентов .NET. Для клиентов JavaScript созданный код прокси автоматически создает учетные записи-посредники для всех концентраторов, существующих на сервере, и регистрирует обработчик, чтобы указать, какие концентраторы клиент планирует использовать. Но для клиента .NET вы создаете прокси-серверы концентратора вручную, поэтому SignalR предполагает, что вы будете использовать любой центр, для которого создается прокси.

В примере кода для подключения к службе SignalR используется URL-адрес по умолчанию "/SignalR". Сведения о том, как указать другой базовый URL-адрес, см. [в разделе ASP.NET SignalR Hub API Guide-Server-URL-адрес/SignalR](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).

Метод `Start` выполняется асинхронно. Чтобы следующие строки кода не выполнялись до тех пор, пока соединение не будет установлено, используйте `await` в асинхронном методе ASP.NET 4,5 или `.Wait()` в синхронном методе. Не используйте `.Wait()` в клиенте WinRT.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

Класс `HubConnection` является потокобезопасным.

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Междоменные соединения от клиентов Silverlight

Сведения о том, как включить междоменные подключения от клиентов Silverlight, см. в разделе [обеспечение доступности службы через границы домена](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>Настройка подключения

Прежде чем устанавливать соединение, можно указать любой из следующих параметров.

- Ограничение количества одновременных подключений.
- Параметры строки запроса.
- Метод перевозки.
- Заголовки HTTP.
- Сертификаты клиента.

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>Установка максимального числа одновременных подключений в клиентах WPF

В клиентах WPF может потребоваться увеличить максимальное число одновременных подключений со значением по умолчанию 2. Рекомендуемое значение — 10.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

Дополнительные сведения см. в разделе [ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>Указание параметров строки запроса

Если требуется отправлять данные на сервер при подключении клиента, можно добавить параметры строки запроса в объект соединения. В следующем примере показано, как задать параметр строки запроса в клиентском коде.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

В следующем примере показано, как считать параметр строки запроса в серверном коде.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>Как указать метод перевозки

В рамках процесса подключения клиент SignalR обычно согласовывается с сервером для определения наилучшего транспорта, поддерживаемого как сервером, так и клиентом. Если вы уже уверены, какой транспорт вы хотите использовать, можно обойти этот процесс согласования. Чтобы указать транспортный метод, передайте объект транспорта в метод Start. В следующем примере показано, как указать метод перевозки в клиентском коде.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

Пространство имен [Microsoft. AspNet. SignalR. Client.](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) Transports содержит следующие классы, которые можно использовать для указания транспорта.

- [лонгполлингтранспорт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [серверсентевентстранспорт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [Вебсоккеттранспорт](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (доступно, только если сервер и клиент используют .NET 4,5).
- [Автотранспортировка](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (автоматически выбирает лучший транспорт, который поддерживается как клиентом, так и сервером. Это транспорт по умолчанию. Передача этого метода в метод `Start` имеет тот же результат, что и не передает ничего.)

Транспорт Фореверфраме не включен в этот список, так как он используется только браузерами.

Сведения о том, как проверить транспортный метод в коде сервера, см. в разделе [ASP.NET SignalR Hub API Guide-Server-как получить сведения о клиенте из свойства Context](../guide-to-the-api/hubs-api-guide-server.md#contextproperty). Дополнительные сведения о транспортировках и резервных запасах см. [в статье Введение в SignalR-транспорты и резервные стратегии](../getting-started/introduction-to-signalr.md#transports).

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>Как указать заголовки HTTP

Чтобы задать заголовки HTTP, используйте свойство `Headers` объекта Connection. В следующем примере показано, как добавить заголовок HTTP.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>Как указать сертификаты клиента

Чтобы добавить сертификаты клиента, используйте метод `AddClientCertificate` объекта Connection.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>Создание прокси-сервера концентратора

Чтобы определить методы на клиенте, которые концентратор может вызывать с сервера, и вызывать методы в концентраторе на сервере, создайте прокси-сервер для концентратора, вызвав `CreateHubProxy` для объекта Connection. Строка, которую вы передаете `CreateHubProxy`, является именем класса концентратора или именем, заданным атрибутом `HubName`, если он использовался на сервере. Сопоставление имен не зависит от регистра.

**Класс Hub на сервере**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**Создание прокси клиента для класса HUB**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

Если класс Hub дополнить атрибутом `HubName`, используйте это имя.

**Класс Hub на сервере**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

**Создание прокси клиента для класса HUB**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

Прокси-объект является потокобезопасным. На самом деле, если вы вызываете `HubConnection.CreateHubProxy` несколько раз с одним и тем же `hubName`, вы получаете один кэшированный объект `IHubProxy`.

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>Определение методов на клиенте, который может вызывать сервер

Чтобы определить метод, который может вызвать сервер, используйте метод `On` прокси-сервера для регистрации обработчика событий.

Сопоставление имен методов не учитывает регистр. Например, `Clients.All.UpdateStockPrice` на сервере будет выполнять `updateStockPrice`, `updatestockprice`или `UpdateStockPrice` на клиенте.

Разные клиентские платформы имеют разные требования к написанию кода метода для обновления пользовательского интерфейса. Приведенные примеры предназначены для клиентов WinRT (Windows Store .NET). Примеры приложений WPF, Silverlight и консольного приложения приведены в [отдельном разделе далее в этом разделе](#wpfsl).

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>Методы без параметров

Если обрабатываемый метод не имеет параметров, используйте неуниверсальную перегрузку метода `On`:

**Код сервера, вызывающий клиентский метод без параметров**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**Клиентский код WinRT для метода, вызываемого с сервера без параметров ([см. примеры WPF и Silverlight далее в этом разделе](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Методы с параметрами, указание типов параметров

Если обрабатываемый метод имеет параметры, укажите типы параметров в качестве универсальных типов метода `On`. Существуют универсальные перегрузки метода `On`, позволяющие указать до 8 параметров (4 в Windows Phone 7). В следующем примере один параметр отправляется в метод `UpdateStockPrice`.

**Серверный код, вызывающий клиентский метод с параметром**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**Класс акции, используемый для параметра**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

**Клиентский код WinRT для метода, вызываемого с сервера с параметром ([см. примеры WPF и Silverlight далее в этом разделе](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Методы с параметрами, указание динамических объектов для параметров

В качестве альтернативы указанию параметров в качестве универсальных типов метода `On` можно указать параметры как динамические объекты:

**Серверный код, вызывающий клиентский метод с параметром**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**Класс акции, используемый для параметра**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

**Клиентский код WinRT для метода, вызываемого с сервера с параметром, с использованием динамического объекта для параметра ([см. примеры WPF и Silverlight далее в этом разделе](#wpfsl))**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>Удаление обработчика

Чтобы удалить обработчик, вызовите его метод `Dispose`.

**Клиентский код для метода, вызываемого с сервера**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**Код клиента для удаления обработчика**

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>Вызов методов сервера из клиента

Чтобы вызвать метод на сервере, используйте метод `Invoke` для прокси-сервера концентратора.

Если метод сервера не имеет возвращаемого значения, используйте неуниверсальную перегрузку метода `Invoke`.

**Серверный код для метода, не имеющего возвращаемого значения**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**Клиентский код, вызывающий метод, не имеющий возвращаемого значения**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

Если метод сервера имеет возвращаемое значение, укажите тип возвращаемого значения в качестве универсального типа метода `Invoke`.

**Серверный код для метода, который имеет возвращаемое значение и принимает параметр сложного типа**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**Класс акции, используемый для параметра и возвращаемого значения**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

**Клиентский код, вызывающий метод с возвращаемым значением и принимающий параметр сложного типа в асинхронном методе ASP.NET 4,5**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**Клиентский код, вызывающий метод с возвращаемым значением и принимающий параметр сложного типа в синхронном методе**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

Метод `Invoke` выполняется асинхронно и возвращает объект `Task`. Если не указать `await` или `.Wait()`, следующая строка кода будет выполняться до завершения выполнения метода, который вызывается.

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>Как работать с событиями времени жизни соединения

SignalR предоставляет следующие события времени жизни подключения, которые можно выполнять:

- `Received`: возникает, когда в соединении получены какие-либо данные. Предоставляет полученные данные.
- `ConnectionSlow`: возникает, когда клиент обнаруживает слишком большое или частое удаление соединения.
- `Reconnecting`: возникает, когда начинается повторное подключение базового транспорта.
- `Reconnected`: возникает при повторном подключении базового транспорта.
- `StateChanged`: возникает при изменении состояния соединения. Предоставляет старое состояние и новое состояние. Сведения о значениях состояния соединения см. в разделе [перечисление ConnectionState](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).
- `Closed`: возникает при отключении соединения.

Например, если требуется отображать предупреждающие сообщения об ошибках, которые не являются критическими, но вызывают периодически возникающих проблем с подключением, например медленная работа или частым удалением соединения, обработайте событие `ConnectionSlow`.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

Дополнительные сведения см. [в разделе Основные сведения и обработка событий времени жизни подключения в SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>Как обрабатывались ошибки

Если на сервере явно не включены подробные сообщения об ошибках, то объект исключения, возвращаемый SignalR после ошибки, содержит минимальные сведения об ошибке. Например, если вызов `newContosoChatMessage` завершается ошибкой, сообщение об ошибке в объекте Error содержит "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Отправка подробных сообщений об ошибках клиентам в рабочей среде не рекомендуется по соображениям безопасности, но если вы хотите включить подробные сообщения об ошибках для устранения неполадок, используйте следующий код на сервере.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

Для обработки ошибок, вызванных SignalR, можно добавить обработчик для события `Error` в объекте Connection.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

Чтобы обрабатывались ошибки вызовов методов, заключите код в блок try-catch.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>Как включить ведение журнала на стороне клиента

Чтобы включить ведение журнала на стороне клиента, задайте свойства `TraceLevel` и `TraceWriter` объекта соединения.

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>Примеры кода приложений WPF, Silverlight и консольного приложения для клиентских методов, которые может вызывать сервер

Примеры кода, показанные выше, для определения клиентских методов, которые сервер может вызывать для клиентов WinRT. В следующих примерах показан эквивалентный код для клиентов WPF, Silverlight и консольных приложений.

### <a name="methods-without-parameters"></a>Методы без параметров

**Клиентский код WPF для метода, вызываемого с сервера без параметров**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**Клиентский код Silverlight для метода, вызываемого с сервера без параметров**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**Код клиента консольного приложения для метода, вызываемого с сервера без параметров**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>Методы с параметрами, указание типов параметров

**Клиентский код WPF для метода, вызываемого с сервера с параметром**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**Клиентский код Silverlight для метода, вызываемого с сервера с параметром**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**Код клиента консольного приложения для метода, вызываемого с сервера с параметром**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>Методы с параметрами, указание динамических объектов для параметров

**Клиентский код WPF для метода, вызываемого с сервера с параметром, с использованием динамического объекта для параметра**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**Клиентский код Silverlight для метода, вызываемого с сервера с параметром, с использованием динамического объекта для параметра**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**Код клиента консольного приложения для метода, вызываемого с сервера с параметром, с использованием динамического объекта для параметра**

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
