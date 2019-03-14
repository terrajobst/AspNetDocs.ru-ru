---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: Устранение неполадок SignalR | Документация Майкрософт
author: bradygaster
description: В этой статье описаны распространенные проблемы с разработкой приложений SignalR.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 38802814fbb748513274f1fd8a33521fafd48ed3
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039411"
---
<a name="signalr-troubleshooting"></a>Устранение неполадок SignalR
====================
по [Патрик Флетчера](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> В этом документе описаны распространенные проблемы с SignalR.
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


Этот документ содержит следующие разделы.

- [Вызов методов между клиентом и сервером без вмешательства пользователя завершается ошибкой](#connection)
- [Настройка WebSocket служб IIS для проверки связи или проверка связи для обнаружения dead клиента](#pong)
- [Другие проблемы с подключением](#other)
- [Ошибки компиляции и на стороне сервера](#server)
- [Проблемы в Visual Studio](#vs)
- [Проблемы Internet Information Services](#iis)
- [Проблемы с Microsoft Azure](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>Вызов методов между клиентом и сервером без вмешательства пользователя завершается ошибкой

В этом разделе описываются возможные причины вызова метода между клиентом и сервером, переход на другой без информативное сообщение об ошибке. В приложении SignalR, сервер не обладает информацией о методах, которые клиент реализует; Когда сервер вызывает клиентский метод, клиенту отправляются данные имени и параметров метода и этот метод выполняется только в том случае, если он существует в формате, который указан сервер. Если отсутствует соответствующий метод находится на стороне клиента, ничего не происходит, и сообщение об ошибке не возникает на сервере.

Для дальнейшей диагностики клиента методов не вызван, можно включить ведение журнала перед вызовом метода, метод start на концентраторе, чтобы увидеть, какие вызовы приходящие с сервера. Чтобы включить ведение журнала в приложении JavaScript, см. в разделе [как включить ведение журнала на стороне клиента (версия клиента JavaScript)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging). Чтобы включить ведение журнала в клиентском приложении .NET, см. в разделе [как включить ведение журнала на стороне клиента (версия клиента .NET)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>Неправильно написанное метода Неверный метод подписи или имя неверные концентратора

Если имя или сигнатуру вызываемого метода полностью соответствует подходящего метода на стороне клиента, вызов завершится ошибкой. Убедитесь, что имя метода, который вызывается сервером совпадает имя метода на стороне клиента. Кроме того, SignalR создает прокси-сервера концентратора, с помощью методов стиле Camel, как и в JavaScript, поэтому вызов метода `SendMessage` на сервере будет называться `sendMessage` в прокси клиента. Если вы используете `HubName` атрибута в коде на стороне сервера, убедитесь, что имя, используемое совпадает имя, используемое для создания концентратора на стороне клиента. Если вы не используете `HubName` атрибут, убедитесь, что имя концентратора в клиенте JavaScript в стиле Camel, например chatHub вместо ChatHub.

### <a name="duplicate-method-name-on-client"></a>Повторяющееся имя метода на клиенте

Убедитесь, что у вас нет повторяющийся метод на клиенте, который отличается только регистром. Если клиентское приложение содержит метод с именем `sendMessage`, убедитесь, что не существует также метод, вызванный `SendMessage` также.

### <a name="missing-json-parser-on-the-client"></a>Отсутствуют средства синтаксического анализа JSON на стороне клиента

SignalR требуется средство синтаксического анализа JSON для сериализации вызовов между сервером и клиентом. Если клиент не имеет встроенные средства синтаксического анализа JSON (например, Internet Explorer 7), необходимо включить его в приложении. Вы можете скачать средство синтаксического анализа JSON [здесь](http://nuget.org/packages/json2).

### <a name="mixing-hub-and-persistentconnection-syntax"></a>Смешивание концентратора и PersistentConnection синтаксиса

SignalR использует две модели обмена данными: Концентраторы и PersistentConnections. Синтаксис вызова этих моделей связи отличается в клиентском коде. Если вы добавили концентратору в коде сервера, убедитесь, что весь код клиента использует синтаксис правильный концентратора.

**Клиентский код JavaScript, создающий PersistentConnection в клиент JavaScript**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**Код клиента JavaScript, который создает прокси-сервер концентратора в клиент Javascript**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**Серверный код на C#, соответствующий маршрут PersistentConnection**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**Серверный код на C#, сопоставляет маршрут к концентратору или несколько концентраторов, при наличии нескольких приложений**

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a>Подключение к работе перед добавлением подписки

Если подключение к концентратору запускается перед добавлением методов, которые могут вызываться с сервера на прокси-сервер, сообщения не будут приниматься. Следующий код JavaScript не запустится концентратор должным образом:

**Неверный код клиента JavaScript, который не позволит концентраторов принимать сообщения**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

Вместо этого добавьте метод подписки перед вызовом начала:

**Код клиента JavaScript, который правильно добавляет подписки к концентратору**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>Отсутствует имя метода в прокси-сервера концентратора

Убедитесь, что метод, определенный на сервере создана подписка на стороне клиента. Несмотря на то, что сервер определяет метод, он по-прежнему должны добавляться к прокси клиента. Методы могут добавляться на прокси-сервер клиента следующим образом (Обратите внимание, что добавляется метод `client` член концентратора, не концентратор напрямую):

**Код клиента JavaScript, который добавляет методы для прокси-сервера-концентратора**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>Концентратор или методов концентратора, не объявлен как Public

Чтобы быть видимым на клиенте, реализации концентратора и методов должны объявляться как `public`.

### <a name="accessing-hub-from-a-different-application"></a>Доступа к концентратору из другого приложения

Концентраторы SignalR может осуществляться только через приложения, реализующие клиентов SignalR. SignalR не может взаимодействовать с другими библиотеками обмен данными (например, SOAP или WCF веб-служб.) Если клиенты не SignalR доступен для целевой платформы, не может непосредственно доступ к конечной точки сервера.

### <a name="manually-serializing-data"></a>Вручную сериализации данных

SignalR будут автоматически использовать JSON для сериализации метод параметры здесь не нужно сделать это самостоятельно.

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>Не выполняется на клиенте в OnDisconnected функции удаленного метода концентратора

Это сделано намеренно. Когда `OnDisconnected` — вызове концентратора уже вошел `Disconnected` состояние, которое больше нельзя вызывать методы концентратора.

**Код сервера C#, который правильно выполняет код в событии OnDisconnected**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a>Не удается инициировать в согласованное время OnDisconnect

Это сделано намеренно. Когда пользователь пытается покинуть страницу с активным соединением SignalR, клиентом SignalR, сделает наиболее безопасным местом для уведомления сервера остановку клиентского соединения. Если клиентом SignalR наилучшей попытки не сможет подключиться к серверу, сервер будет освободить соединение после настраиваемое `DisconnectTimeout` позже, после чего `OnDisconnected` событие будет срабатывать. Если клиентом SignalR усилия попытка окажется успешной, `OnDisconnected` событие будет срабатывать немедленно.

Сведения об установке `DisconnectTimeout` настройки, см. в разделе [обработка событий времени существования подключений: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout).

### <a name="connection-limit-reached"></a>Достигнут предел подключения

При использовании полной версии IIS в клиентской операционной системе, например Windows 7, накладывается ограничение в 10-подключений. При использовании операционной системы клиента, используйте IIS Express во избежание этого ограничения.

### <a name="cross-domain-connection-not-set-up-properly"></a>Подключение между доменами настроены неверно

Если соединение между доменами (соединение, для которого SignalR URL-адрес не находится в том же домене, что и страница размещения) не установлено правильно, соединение может выдать сбой без сообщения об ошибке. Сведения о том, как для обеспечения взаимодействия между доменами, см. в разделе [как для установления соединения между доменами](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>Подключение с помощью NTLM (Active Directory) не работает в клиент .NET

Подключения в клиентском приложении .NET, которая использует безопасность домена может завершиться ошибкой, если подключение не настроено должным образом. Для использования SignalR в доменной среде, задайте свойство необходимые соединения следующим образом:

**Клиентский код на C#, реализующий учетные данные для подключения**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a>Настройка WebSocket служб IIS для проверки связи или проверка связи для обнаружения dead клиента

SignalR серверы не знаете, если клиент очередь недоставленных или нет, и они полагаются на уведомления от базового веб-ошибками соединения, то есть, `OnClose` обратного вызова. Одним из решений этой проблемы является настройка WebSocket служб IIS для выполнения проверки связи или проверка связи для вас. Это гарантирует, что подключение будет закрыто, если оно нарушает работу неожиданно. Дополнительные сведения см. в разделе [публикация на сайте stackoverflow](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss).

<a id="other"></a>

## <a name="other-connection-issues"></a>Другие проблемы с подключением

В этом разделе описываются причины и способы устранения конкретных проблем или сообщений об ошибках, возникающих во время подключения.

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>Ошибка «Start должен вызываться перед отправкой данных»

Эта ошибка обычно возникает, если код ссылается на объекты SignalR, прежде чем подключение будет запущена. Присоединит для обработчиков и прочее, будут вызывать методы, определенные на сервере необходимо добавить после создания подключения. Обратите внимание, что вызов `Start` осуществляется асинхронно, поэтому код после вызова может выполняться до его завершения. Для добавления обработчиков, после подключения запуска полностью рекомендуется поместить их в функции обратного вызова, который передается как параметр метода start:

**Клиентский код JavaScript, который правильно добавляет обработчики событий, которые ссылаются на объекты SignalR**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

Эта ошибка также могут отображаться, если соединение останавливается, хотя по-прежнему ссылаются объекты SignalR.

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>«301 перемещено навсегда» или «временно перемещен 302» ошибка

Эта ошибка может возникать, если проект содержит папку с именем SignalR, в которой будет мешать автоматически создается прокси-сервер. Чтобы избежать этой ошибки, не используйте папку с именем `SignalR` в приложении, или создание автоматического прокси-сервера включите off. См. в разделе [созданного прокси и что он делает для вас](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) для получения дополнительных сведений.

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>Ошибка «403 запрещено» в клиенте .NET и Silverlight

Эта ошибка может возникать в средах между доменами, взаимодействие между доменами не поддерживающих должным образом. Сведения о том, как для обеспечения взаимодействия между доменами, см. в разделе [как для установления соединения между доменами](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain). Для установления соединения между доменами в клиенте Silverlight, см. в разделе [междоменные подключения от клиентов Silverlight](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).

### <a name="404-not-found-error"></a>Ошибка «404 не найдено»

Существует несколько причин этой проблемы. Проверьте все указанные ниже:

- **Адрес прокси-сервера концентратора ссылку неправильный формат:** Эта ошибка обычно возникает, если ссылку на созданный концентратор прокси-адрес имеет неправильный. Убедитесь, что ссылка на адрес центра создается правильно. См. в разделе [способ создания ссылок динамически формируемых прокси-](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) подробные сведения.
- **Добавление маршрутов для приложения, прежде чем добавлять маршрут концентратора:** Если приложение использует другие маршруты, убедитесь, что первый маршрут добавлен вызов `MapSignalR`.
- **С помощью IIS 7 или 7.5 без обновления для URL-адреса приложения без расширений.** С помощью IIS 7 или 7.5 требуется обновление для URL-адреса без расширений приложения таким образом, сервер может предоставлять доступ к определениям концентратора в `/signalr/hubs`. Обновление можно найти [здесь](https://support.microsoft.com/kb/980368).
- **Кэш IIS устарели или повреждены:** Чтобы убедиться, что содержимое кэша не являются устаревшими, введите следующую команду в окне PowerShell, чтобы очистить кэш:

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a>«500 Внутренняя ошибка сервера»

Это очень Общая ошибка, которая может иметь самые разнообразные причины. Сведения об ошибке должно отображаться в журнале событий сервера, или можно найти по отладку сервера. Более подробные сведения об ошибке можно получить, включив подробные сведения об ошибках на сервере. Дополнительные сведения см. в разделе [способ обработки ошибок в классе центр](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).

Эта ошибка обычно возникает, если брандмауэр или прокси-сервер не настроен правильно, вызывая заголовки запроса для перезаписи. Решение заключается в том, чтобы убедиться в том, что порт 80 включен брандмауэр или прокси-сервера.

### <a name="unexpected-response-code-500"></a>«Код неожиданный ответ: 500"

Эта ошибка может возникать, если версия .NET framework, используемой в приложении не соответствует версии, указанной в файле Web.Config. Решение заключается в том, чтобы убедиться, что в настройках приложения и файл Web.Config используется .NET 4.5.

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>«TypeError: &lt;hubType&gt; не определено» ошибка

Это ошибка возникнет при вызове `MapSignalR` не выполняется должным образом. См. в разделе [как зарегистрировать по промежуточного слоя SignalR и настроить параметры SignalR](../guide-to-the-api/hubs-api-guide-server.md#route) Дополнительные сведения.

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException было обработано пользовательским кодом

Убедитесь, что параметры, которые можно отправить в методы содержит не поддерживают сериализацию типов (таких как дескрипторы файлов или подключения к базе данных). Если вам нужно использовать члены объекта на стороне сервера, вы не хотите отправить клиенту (либо для обеспечения безопасности, либо в целях сериализации), используйте `JSONIgnore` атрибута.

### <a name="protocol-error-unknown-transport-error"></a>«Ошибка протокола: Ошибка Неизвестный транспорта»

Эта ошибка может возникать, если клиент не поддерживает транспорты, которые использует SignalR. См. в разделе [транспорта и в случае ошибки](../getting-started/introduction-to-signalr.md#transports) сведения, на котором браузеры можно использовать с SignalR.

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>«Отключено создание прокси JavaScript концентратора.»

Эта ошибка возникает в том случае, если `DisableJavaScriptProxies` задается при также включая ссылку на динамически созданный прокси в `signalr/hubs`. Дополнительные сведения о создании прокси-сервер вручную, см. в разделе [созданный прокси и что он делает для вас](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>«Идентификатор подключения имеет неправильный формат» или «удостоверение пользователя нельзя изменить во время подключения SignalR» ошибка

Эта ошибка может возникать, если используется проверка подлинности и выходе клиента, прежде чем подключение остановлен. Решение, необходимо остановить соединение перед при выходе клиента SignalR.

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>«Никаким кодом не перехватывается ошибка: SignalR: jQuery не найден. Ошибка, убедитесь, что существует jQuery, прежде чем файл SignalR.js»

SignalR JavaScript клиенту требуется jQuery для выполнения. Убедитесь, что справочной информации для jQuery указан правильно, что путь, используемый является допустимым, и ссылку на jQuery предшествует ссылку SignalR.

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>«Неперехваченное TypeError: Не удается прочитать свойство "&lt;свойство&gt;" неопределенное» ошибка

Эта ошибка результатом отсутствия jQuery или центров прокси-сервера, правильность ссылок. Убедитесь, что справочной информации для jQuery и центров прокси-сервера указан правильно, что путь, используемый является допустимым, и ссылку на jQuery предшествует ссылку центров прокси-сервер. Ссылку по умолчанию на центров прокси-сервер должен иметь следующий вид:

**Код на стороне клиента HTML, который правильно ссылается на центров прокси-сервера**

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>Ошибка «RuntimeBinderException было обработано пользовательским кодом»

Эта ошибка может возникать при неверные перегрузку `Hub.On` используется. Если метод имеет возвращаемое значение, тип возвращаемого значения необходимо указывать в качестве параметра универсального типа:

**Метод, определенный на клиенте (без созданный прокси-сервера)**

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>Идентификатор соединения не согласована, или разрыва соединения между загрузок страниц

Это сделано намеренно. Так как объект концентратора размещается в объект страницы, концентратор уничтожается при обновлении этой страницы. Приложению многостраничных для поддержания связи между пользователями и идентификаторов подключений, чтобы они будут согласованы между загрузок страниц. Идентификаторов подключений, которые могут храниться на сервере в любом `ConcurrentDictionary` объекта или базу данных.

### <a name="value-cannot-be-null-error"></a>Ошибка «Значение не может быть null»

Методы на стороне сервера с необязательными параметрами в настоящее время не поддерживаются; Если указан необязательный параметр, метод завершится с ошибкой. Дополнительные сведения см. в разделе [необязательные параметры](https://github.com/SignalR/SignalR/issues/324).

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>«Firefox не удается установить подключение к серверу по адресу &lt;адрес&gt;"Ошибка в Firebug

Это сообщение об ошибке может отображаться в Firebug, если происходит сбой согласования транспорта WebSocket и вместо него используется другой протокол. Это сделано намеренно.

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>Ошибка «удаленный сертификат недействителен согласно процедуре проверки» в клиентском приложении .NET

Если сервер требует настраиваемых клиентских сертификатов, затем можно добавить x509certificate соединение перед выполнением запроса. Добавить сертификат для соединения с помощью `Connection.AddClientCertificate`.

### <a name="connection-drops-after-authentication-times-out"></a>После проверки подлинности истекает разрыва подключения

Это сделано намеренно. Учетные данные проверки подлинности нельзя изменить, если подключение активно; Чтобы обновить учетные данные, соединение необходимо остановить и перезапустить.

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>OnConnected вызывается два раза в том случае, когда с помощью jQuery Mobile

jQuery Mobile `initializePage` функция принудительно выполняет скрипты на каждой странице, чтобы выполнить повторно, тем самым создавая второе подключение. Решения этой проблемы включают в себя:

- Включайте ссылку на jQuery Mobile перед в файле JavaScript.
- Отключить `initializePage` функции, задав `$.mobile.autoInitializePage = false`.
- Подождите, пока страница для завершения инициализации, прежде чем выполнять подключение.

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>Сообщения задержаны в приложениях Silverlight, с помощью отправки событий сервера

Сообщения задержаны в том случае, при использовании сервера пересылке событий Silverlight. Чтобы принудительно длинный опрос для использования вместо этого, используйте следующие параметры при запуске соединения.

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>С помощью «Разрешение Denied» навсегда кадра протокола

Это известная проблема, описано [здесь](https://github.com/SignalR/SignalR/issues/1963). Эта проблема может возникать, используя последнюю версию библиотеки JQuery; обойти это можно понизить приложению JQuery 1.8.2.

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a>"InvalidOperationException: Не допустимый запрос веб-сокета.

Эта ошибка может возникать, если используется протокол WebSocket, но сетевой прокси-сервер изменяет заголовки запроса. Решение заключается в том, чтобы настроить прокси-сервера для веб-сокет на порт 80.

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a>«Исключение: &lt;имя метода&gt; метод не удалось разрешить» когда клиент вызывает метод на сервере

Эта ошибка может быть результатом использования типов данных, которые не могут быть обнаружены в полезные данные JSON, например массив. Решение — использовать тип данных, который может быть обнаружен по JSON, например, IList. Дополнительные сведения см. в разделе [клиент .NET, не может вызывать методы концентратора с помощью параметров-массивов](https://github.com/SignalR/SignalR/issues/2672).

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>Ошибки компиляции и на стороне сервера

 В следующем разделе приведены возможные решения для компилятора и ошибки времени выполнения на стороне сервера.

### <a name="reference-to-hub-instance-is-null"></a>Ссылка на экземпляр концентратора имеет значение null

Так как для каждого подключения, создается экземпляр концентратора не может создавать экземпляр концентратора в коде самостоятельно. Для вызова методов в концентратор из за пределами сам концентратор, см. в разделе [как вызывать методы клиента и управлять ими групп за пределами классу Hub](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) способ получить ссылку на контекст концентратора.

### <a name="httpcontextcurrentsession-is-null"></a>HTTPContext.Current.Session имеет значение null

Это сделано намеренно. SignalR поддерживает состояние сеанса ASP.NET, так как Включение состояния сеанса нарушит дуплексного обмена сообщениями.

### <a name="no-suitable-method-to-override"></a>Нет метод, пригодный для переопределения

Эта ошибка может возникнуть при использовании кода из более старой документации и в блогах. Убедитесь, что вы не ссылаются на имена методов, которые изменились или устарели (например `OnConnectedAsync`).

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostContextExtensions.WebSocketServerUrl имеет значение null

Это сделано намеренно. Этот член является устаревшим и не должны использоваться.

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>Ошибка «маршрут с именем «signalr.hubs» уже находится в коллекции маршрутов»

Эта ошибка возникает, если `MapSignalR` вызывается дважды вашим приложением. Некоторые приложения вызывают пример `MapSignalR` непосредственно в классе Startup; другим пользователям в вызове в класс-оболочку. Убедитесь, что приложение не оба.

### <a name="websocket-is-not-used"></a>WebSocket не используется

Если вы убедились, что сервер и клиенты отвечают требованиям для WebSocket (перечисленных в [поддерживаемые платформы](../getting-started/supported-platforms.md) документа), вам потребуется включить WebSocket на сервере. Инструкции для этого можно найти [здесь](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).

### <a name="connection-is-undefined"></a>$.connection не определено

Эта ошибка указывает, что скрипты на странице не загружены правильно, или прокси-сервера концентратора недоступен или осуществляется неправильно. Убедитесь, что ссылки на скрипты на странице соответствуют скрипты, загруженные в проекте и /signalr/hubs, которые может осуществляться в браузере, когда сервер работает.

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a>Не удается найти один или несколько типов, необходимых для компиляции динамического выражения

Эта ошибка указывает, что `Microsoft.CSharp` отсутствует библиотека. Добавьте его в **сборок -&gt;Framework** вкладки.

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a>Состояние вызывающего объекта нельзя обращаться из Clients.Caller в Visual Basic или в строго типизированный центра; Ошибка «Недопустимое преобразование из типа «Task (Of Object)» в тип «String»»

Чтобы получить состояние вызывающего объекта в Visual Basic или в строго типизированный концентратора, используйте `Clients.CallerState` (впервые представлено в SignalR 2.1) вместо свойства `Clients.Caller`.

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Проблемы в Visual Studio

В этом разделе описываются проблемы, возникающие в Visual Studio.

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>Сценарий узла "документы" не отображается в обозревателе решений

Некоторые из наших учебниках дать вам ссылки на узел «Документы скриптов» в обозревателе решений во время отладки. Этот узел создается в отладчике JavaScript и отображается только при отладке клиентов браузера Internet Explorer; узел не будет отображаться, если используются Chrome или Firefox. Отладчик JavaScript также не запустится, если выполняется другой отладчик клиента, такие как отладчик Silverlight.

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR не работает в Visual Studio 2008 или более ранней версии

Это сделано намеренно. SignalR требуется платформа .NET Framework 4 или более поздней версии; для этого необходимо разрабатывать приложений SignalR в Visual Studio 2010 или более поздней версии. Серверный компонент служб SignalR требуется .NET Framework 4.5.

<a id="iis"></a>

## <a name="iis-issues"></a>Проблемы с IIS

Этот раздел содержит проблемы с Internet Information Services.

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a>SignalR работает с Visual Studio development server, но не в службах IIS

SignalR поддерживается в IIS 7.0 и 7.5, но поддержка URL-адреса без расширений приложения необходимо добавить. Чтобы добавить поддержку без расширений URL-адресов, см. в разделе [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)

SignalR требует ASP.NET для установки на сервере (ASP.NET не установлена на сервере IIS по умолчанию). Чтобы установить ASP.NET, см. в разделе [загрузок ASP.NET](https://www.asp.net/downloads).

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a>Проблемы с Microsoft Azure

Этот раздел содержит проблемы с Microsoft Azure.

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a>FileLoadException при размещении SignalR в рабочей роли Azure

Размещение SignalR в рабочей роли Azure может привести к исключение «не удалось загрузить файл или сборку "Microsoft.Owin, Version = 2.0.0.0». Это известная проблема с помощью NuGet; Перенаправление привязки не добавляются автоматически в проектах рабочей роли Azure. Чтобы устранить эту проблему, можно вручную добавить переадресации привязок. Добавьте следующие строки `app.config` файл проекта рабочей роли.

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>Сообщения не принимаются через Azure задней панели после изменения имена разделов

Разделы, используемые Azure объединительной платы хранятся в системе; они не предназначены для настройки пользователя.