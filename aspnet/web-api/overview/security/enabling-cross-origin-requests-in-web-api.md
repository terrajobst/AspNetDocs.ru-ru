---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: Включение запросов между источниками в веб-API ASP.NET 2 | Документация Майкрософт
author: MikeWasson
description: Показывает, как поддерживать общий доступ к ресурсам между источниками (CORS) в веб-API ASP.NET.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447618"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a>Включить запросы между источниками в веб-API ASP.NET 2

по [Майк Уоссон](https://github.com/MikeWasson)

> Параметры безопасности веб-браузера предотвращают отправку запросов AJAX с веб-страницы к другому домену. Это ограничение называется *политикой того же происхождения*и предотвращает чтение вредоносных данных с другого сайта злоумышленником. Однако иногда может потребоваться разрешить другим сайтам вызывать веб-API.
>
> [Общий доступ к ресурсам в разных источниках](http://www.w3.org/TR/cors/) (CORS) — это стандарт консорциума W3C, позволяющий серверу смягчить ту же политику. С помощью CORS сервер может явным образом разрешить некоторые запросы независимо от источника, а другие — отклонить. CORS безопаснее и более гибкий, чем более ранние методики, такие как [JSONP](http://en.wikipedia.org/wiki/JSONP). В этом руководстве показано, как включить CORS в приложении веб-API.
>
> ## <a name="software-used-in-the-tutorial"></a>Программное обеспечение, используемое в этом руководстве
>
> - [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Веб-API 2,2

## <a name="introduction"></a>Введение

В этом руководстве демонстрируется поддержка CORS в веб-API ASP.NET. Начнем с создания двух проектов ASP.NET — один под названием «WebService», который размещает контроллер веб-API, а другой — «WebClient», который вызывает WebService. Поскольку два приложения размещаются в разных доменах, запрос AJAX от WebClient к WebService является запросом между источниками.

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a>Что такое "тот же источник"?

Два URL-адреса имеют один и тот же источник, если они имеют идентичные схемы, узлы и порты. ([RFC 6454](http://tools.ietf.org/html/rfc6454))

Эти два URL-адреса имеют один и тот же источник:

- `http://example.com/foo.html`
- `http://example.com/bar.html`

Эти URL-адреса имеют разные источники, отличные от предыдущих двух:

- `http://example.net`-другой домен
- `http://example.com:9000/foo.html`-другой порт
- Другая схема `https://example.com/foo.html`
- `http://www.example.com/foo.html`-различные поддомены

> [!NOTE]
> При сравнении источников Internet Explorer не учитывает порт.

## <a name="create-the-webservice-project"></a>Создание проекта WebService

> [!NOTE]
> В этом разделе предполагается, что вы уже знакомы с созданием проектов веб-API. Если нет, см. раздел [Начало работы with веб-API ASP.NET](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).

1. Запустите Visual Studio и создайте проект **веб-приложения ASP.NET (.NET Framework)** .
2. В диалоговом окне **Создание веб-приложения ASP.NET** выберите **пустой** шаблон проекта. В разделе **Добавление папок и основных ссылок для**установите флажок **веб-API** .

   ![Диалоговое окно создания проекта ASP.NET в Visual Studio](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. Добавьте контроллер веб-API с именем `TestController` со следующим кодом:

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. Приложение можно запустить локально или развернуть в Azure. (Для снимков экрана в этом руководстве приложение развертывается в веб-приложениях службы приложений Azure.) Чтобы убедиться, что веб-API работает, перейдите по адресу `http://hostname/api/test/`, где *HostName* — это домен, в котором развернуто приложение. Вы увидите текст ответа &quot;получить: тестовое сообщение&quot;.

   ![Веб-браузер, демонстрирующий тестовое сообщение](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a>Создание проекта WebClient

1. Создайте другой проект **веб-приложения ASP.NET (.NET Framework)** и выберите шаблон проекта **MVC** . При необходимости выберите **изменить проверку Подлинности** > **без проверки подлинности**. Для работы с этим руководством не требуется проверка подлинности.

   ![Шаблон MVC в диалоговом окне создания проекта ASP.NET в Visual Studio](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. В **Обозреватель решений**откройте файл *Views/Home/Index. cshtml*. Замените код в этом файле следующим кодом:

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   Для переменной *serviceUrl* используйте URI приложения WebService.

3. Запустите приложение WebClient локально или опубликуйте его на другом веб-сайте.

При нажатии кнопки "попробовать" запрос AJAX отправляется в приложение WebService с помощью метода HTTP, указанного в раскрывающемся списке (GET, POST или поместить). Это позволяет проверять различные запросы между источниками. В настоящее время приложение WebService не поддерживает CORS, поэтому при нажатии кнопки вы получите сообщение об ошибке.

![Ошибка "попробовать" в браузере](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> Если вы видите HTTP-трафик в таком средстве, как [Fiddler](https://www.telerik.com/fiddler), вы увидите, что браузер ОТПРАВЛЯЕТ запрос GET, и запрос завершается, но вызов AJAX возвращает ошибку. Важно понимать, что политика того же источника не мешает обозревателю *отправлять* запрос. Вместо этого он предотвращает просмотр *ответа*приложением.

![Веб-отладчик Fiddler, отображающий веб-запросы](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a>Включение CORS

Теперь включите CORS в приложении WebService. Сначала добавьте пакет NuGet для CORS. В Visual Studio в меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне консоли диспетчера пакетов введите следующую команду:

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

Эта команда устанавливает последний пакет и обновляет все зависимости, включая основные библиотеки веб-API. Используйте флаг `-Version`, чтобы выбрать конкретную версию. Для пакета CORS требуется веб-API 2,0 или более поздней версии.

Откройте файл *App\_Start/WebApiConfig. CS*. Добавьте следующий код в метод **WebApiConfig. Register** :

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

Затем добавьте атрибут **[EnableCors]** в класс `TestController`:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

В качестве параметра *происхождения* используйте URI, в котором развернуто приложение WebClient. Это позволяет выполнять запросы между источниками от WebClient, не разрешая все остальные междоменные запросы. Позже я опишу параметры для **[EnableCors]** более подробно.

Не включайте косую черту в конце URL-адреса *происхождения* .

Повторно разверните обновленное приложение WebService. Обновлять WebClient не требуется. Теперь запрос AJAX от WebClient должен быть выполнен. Методы GET, WHERE и POST разрешены.

![Веб-браузер, показывающий успешное тестовое сообщение](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a>Принцип работы CORS

В этом разделе описывается, что происходит в запросе CORS на уровне HTTP-сообщений. Важно понимать, как работает CORS, чтобы можно было правильно настроить атрибут **[EnableCors]** и устранять неполадки, если они не работают должным образом.

Спецификация CORS вводит несколько новых HTTP-заголовков, которые позволяют выполнять запросы между источниками. Если браузер поддерживает CORS, эти заголовки автоматически устанавливаются для запросов между источниками. Вам не нужно ничего делать в коде JavaScript.

Ниже приведен пример запроса между источниками. Заголовок "Origin" предоставляет домен сайта, выполняющего запрос.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

Если сервер разрешает запрос, он устанавливает заголовок Access-Control-Allow-Origin. Значение этого заголовка либо соответствует заголовку источника, либо является подстановочным значением «\*», что означает, что любой источник разрешен.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

Если ответ не включает заголовок Access-Control-Allow-Origin, то запрос AJAX завершается ошибкой. В частности, браузер не разрешает запрос. Даже если сервер возвращает успешный ответ, браузер не делает ответ доступным клиентскому приложению.

**Предпечатные запросы**

Для некоторых запросов CORS браузер отправляет дополнительный запрос, называемый «предварительным запросом», перед отправкой фактического запроса ресурса.

Браузер может пропустить Предпечатный запрос, если выполняются следующие условия.

- Метод запроса — GET, HEAD или POST, *а*
- Приложение не устанавливает никаких заголовков запроса, кроме Accept, Accept-Language, Content-Language, Content-Type или Last-Event-ID, *и*
- Заголовок Content-Type (если задан) является одним из следующих:

    - application/x-www-form-urlencoded
    - multipart/form-data
    - text/plain

Правило о заголовках запросов применяется к заголовкам, которые устанавливаются приложением путем вызова **сетрекуессеадер** для объекта **XMLHttpRequest** . (Спецификация CORS вызывает эти "заголовки запроса автора".) Правило не применяется к заголовкам, которые может задать *браузер* , например агент пользователя, узел или длина содержимого.

Ниже приведен пример предпечатного запроса:

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

Запрос перед рейсом использует метод HTTP OPTIONS. Он включает два специальных заголовка:

- Access-Control-Request-method — метод HTTP, который будет использоваться для фактического запроса.
- Access-Control-request-headers. список заголовков запросов, установленных *приложением* в фактическом запросе. (Опять же, сюда не входят заголовки, задаются браузером.)

Ниже приведен пример ответа, предполагая, что сервер разрешает запрос:

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

Ответ содержит заголовок Access-Control-Allow-Methods, в котором перечислены допустимые методы и при необходимости заголовок Access-Control-Allow-Headers, который перечисляет разрешенные заголовки. Если Предпечатный запрос выполнен, браузер отправляет фактический запрос, как описано выше.

Средства, обычно используемые для тестирования конечных точек с запросами параметров предварительной проверки (например, [Fiddler](https://www.telerik.com/fiddler) и [POST](https://www.getpostman.com/)), не отправляют обязательные заголовки параметров по умолчанию. Убедитесь, что заголовки `Access-Control-Request-Method` и `Access-Control-Request-Headers` отправлены с запросом, а заголовки параметров достигают приложения через IIS.

Чтобы настроить службы IIS таким образом, чтобы приложение ASP.NET получало и обрабатывал запросы параметров, добавьте следующую конфигурацию в файл *Web. config* приложения в разделе `<system.webServer><handlers>`:

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

Удаление `OPTIONSVerbHandler` предотвращает обработку запросов параметров службами IIS. Замена `ExtensionlessUrlHandler-Integrated-4.0` позволяет запросам параметров обращаться к приложению, так как регистрация модуля по умолчанию разрешает только запросы GET, HEAD, POST и DEBUG с URL-адресами без расширений.

## <a name="scope-rules-for-enablecors"></a>Правила области для [EnableCors]

Можно включить CORS для каждого действия, для каждого контроллера или глобально для всех контроллеров веб-API в приложении.

**За действие**

Чтобы включить CORS для одного действия, установите атрибут **[EnableCors]** в методе действия. В следующем примере CORS включается только для метода `GetItem`.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

**На контроллер**

Если задать **[EnableCors]** в классе контроллера, он будет применяться ко всем действиям на контроллере. Чтобы отключить CORS для действия, добавьте к действию атрибут **[дисаблекорс]** . В следующем примере показано включение CORS для каждого метода, кроме `PutItem`.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

**Разместил**

Чтобы включить CORS для всех контроллеров веб-API в приложении, передайте экземпляр **енаблекорсаттрибуте** в метод **EnableCors** :

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

Если задать атрибут более чем в одной области, порядок приоритета будет следующим:

1. Действие
2. Контроллер
3. Global

## <a name="set-the-allowed-origins"></a>Установка разрешенных источников

Параметр *Origins* атрибута **[EnableCors]** указывает, каким источникам разрешен доступ к ресурсу. Значение представляет собой разделенный запятыми список разрешенных источников.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

Можно также использовать подстановочное значение "\*", чтобы разрешить запросы из любых источников.

Следует тщательно продуматьсь перед разрешением запросов из любого источника. Это означает, что буквально любой веб-сайт может выполнять вызовы AJAX к веб-API.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a>Задание допустимых методов HTTP

Параметр *Methods* атрибута **[EnableCors]** указывает, какие методы HTTP могут получать доступ к ресурсу. Чтобы разрешить все методы, используйте подстановочное значение "\*". В следующем примере допускаются только запросы GET и POST.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a>Задание разрешенных заголовков запроса

В этой статье ранее было описано, как предварительный запрос может содержать заголовок Access-Control-request-headers, в котором перечислены заголовки HTTP, заданные приложением (так называемый «заголовки запроса автора»). Параметр *headers* атрибута **[EnableCors]** указывает, какие заголовки запроса автора разрешены. Чтобы разрешить любой заголовок, задайте для *заголовков* значение "\*". Чтобы список разрешений определенные заголовки, установите для *заголовков* разделенный запятыми список разрешенных заголовков:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

Однако браузеры не полностью согласуются с тем, как они устанавливают заголовки Access-Control-request-headers. Например, Chrome в настоящее время включает "источник". FireFox не включает стандартные заголовки, такие как "Accept", даже если приложение задает их в скрипте.

Если для *заголовков* заданы любые значения, отличные от "\*", следует включить по меньшей мере "Accept", "Content-Type" и "Origin", а также любые настраиваемые заголовки, которые требуется поддерживать.

## <a name="set-the-allowed-response-headers"></a>Задание разрешенных заголовков ответа

По умолчанию браузер не предоставляет приложению все заголовки ответа. По умолчанию доступны заголовки ответов:

- Cache-Control;
- Content-Language;
- Content-Type
- Expires
- Последний измененный
- Включают

Спецификация CORS вызывает эти [простые заголовки ответа](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header). Чтобы сделать другие заголовки доступными для приложения, задайте параметр *exposedHeaders* **[EnableCors]** .

В следующем примере метод `Get` контроллера задает пользовательский заголовок с именем "X-Custom-Header". По умолчанию браузер не будет предоставлять этот заголовок в запросе между источниками. Чтобы сделать заголовок доступным, включите "X-Custom-Header" в *exposedHeaders*.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a>Передача учетных данных в запросах между источниками

Учетные данные требует специальной обработки в запросе CORS. По умолчанию браузер не отправляет учетные данные с запросом между источниками. Учетные данные включают файлы cookie, а также схемы проверки подлинности HTTP. Чтобы отправить учетные данные с запросом между источниками, клиент должен установить для **XMLHttpRequest. вискредентиалс** значение true.

Непосредственное использование **XMLHttpRequest** :

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

В jQuery:

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

Кроме того, сервер должен разрешать учетные данные. Чтобы разрешить учетные данные для разных источников в веб-API, задайте для свойства **суппортскредентиалс** атрибута **[EnableCors]** значение true:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

Если это свойство имеет значение true, ответ HTTP будет включать заголовок Access-Control-Allow-Credentials. Этот заголовок сообщает браузеру, что сервер разрешает учетные данные для запроса между источниками.

Если браузер отправляет учетные данные, но ответ не включает допустимый заголовок Access-Control-Allow-Credential, браузер не будет предоставлять ответ приложению, а запрос AJAX завершится ошибкой.

Будьте внимательны при установке параметра **суппортскредентиалс** в значение true, так как это означает, что веб-сайт в другом домене может отправить учетные данные пользователя, выполнившего вход, в веб-интерфейс API от имени пользователя без уведомления пользователя. В спецификации CORS также указано, что установка *источников* на &quot;\*&quot; недопустима, если **суппортскредентиалс** имеет значение true.

## <a name="custom-cors-policy-providers"></a>Пользовательские поставщики политик CORS

Атрибут **[EnableCors]** реализует интерфейс **икорсполиципровидер** . Вы можете предоставить собственную реализацию, создав класс, производный от **Attribute** , и реализующий **икорсполиципровидер**.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

Теперь можно применить атрибут в любом месте, которое вы бы поместили **[EnableCors]** .

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

Например, Пользовательский поставщик политики CORS может считывать параметры из файла конфигурации.

В качестве альтернативы использованию атрибутов можно зарегистрировать объект **икорсполиципровидерфактори** , создающий объекты **икорсполиципровидер** .

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

Чтобы задать **икорсполиципровидерфактори**, вызовите метод расширения **сеткорсполиципровидерфактори** при запуске, как показано ниже.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a>Поддержка браузеров

Пакет CORS веб-API — это технология на стороне сервера. Браузер пользователя также должен поддерживать CORS. К счастью, текущие версии всех основных браузеров включают [поддержку CORS](http://caniuse.com/cors).
