---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: Работа с SSL в веб-API | Документация Майкрософт
author: MikeWasson
description: Показывает, как использовать SSL с веб-API ASP.NET, в том числе с помощью SSL-сертификатов клиента.
ms.author: riande
ms.date: 02/22/2019
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 31589b3713b1f1a9b98d12906bfef81f8bf5e3f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484416"
---
# <a name="working-with-ssl-in-web-api"></a>Работа с SSL в веб-API

по [Майк Уоссон](https://github.com/MikeWasson)

Несколько распространенных схем проверки подлинности не являются безопасными по сравнению с простым HTTP. В частности, базовая проверка подлинности и формы проверки подлинности отправляют незашифрованные учетные данные. Для обеспечения безопасности эти схемы проверки подлинности *должны* использовать SSL. Кроме того, для проверки подлинности клиентов можно использовать SSL-сертификаты клиентов.

## <a name="enabling-ssl-on-the-server"></a>Включение SSL на сервере

Чтобы настроить SSL в IIS 7 или более поздней версии, выполните следующие действия.

- Создайте или получите сертификат. Для тестирования можно создать самозаверяющий сертификат.
- Добавьте привязку HTTPS.

Дополнительные сведения см. в разделе [Настройка SSL в IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

Для локального тестирования можно включить SSL в IIS Express из Visual Studio. В окно свойств задайте для параметра **SSL Enabled** значение **true**. Обратите внимание на значение **URL-адреса SSL**. Используйте этот URL-адрес для проверки соединений HTTPS.

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a>Применение SSL в контроллере веб-API

При наличии привязки HTTPS и HTTP клиенты по-прежнему могут использовать HTTP для доступа к сайту. Вы можете разрешить доступ к некоторым ресурсам по протоколу HTTP, а другие ресурсы — по протоколу SSL. В этом случае используйте фильтр действий, чтобы требовать SSL для защищенных ресурсов. В следующем коде показан фильтр проверки подлинности веб-интерфейса API, проверяющий SSL-подключения.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

Добавьте этот фильтр в любое действие веб-интерфейса API, для которого требуется SSL:

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a>SSL-сертификаты клиентов

Протокол SSL обеспечивает проверку подлинности с помощью сертификатов инфраструктуры открытых ключей. Сервер должен предоставить сертификат, проверяющий подлинность сервера для клиента. Чаще всего клиент предоставляет сертификат серверу, но это один из вариантов проверки подлинности клиентов. Чтобы использовать сертификаты клиента с SSL, необходим способ распространения подписанных сертификатов пользователям. Для многих типов приложений это не будет хорошим интерфейсом пользователя, но в некоторых средах (например, на предприятии) это может быть возможным.

| Преимущества | Недостатки |
| --- | --- |
| — Учетные данные сертификата надежнее, чем имя пользователя и пароль. — Протокол SSL обеспечивает полный безопасный канал с проверкой подлинности, целостностью сообщений и шифрованием сообщений. | — Необходимо получить сертификаты PKI и управлять ими. — Клиентская платформа должна поддерживать SSL-сертификаты клиентов. |

Чтобы настроить службы IIS для приема сертификатов клиентов, откройте Диспетчер IIS и выполните следующие действия.

1. Щелкните узел сайта в представлении в виде дерева.
2. Дважды щелкните компонент **Параметры SSL** в средней области.
3. В разделе **Сертификаты клиента**выберите один из следующих вариантов. 

    - **Принять**: IIS будет принимать сертификат от клиента, но не требует его.
    - **Требовать**: требовать сертификат клиента. (Чтобы включить этот параметр, необходимо также выбрать "требовать SSL").

Эти параметры также можно задать в файле ApplicationHost. config:

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

Флаг **сслнеготиатецерт** означает, что IIS будет принимать сертификат от клиента, но не требует его (аналогично параметру Accept в диспетчере служб IIS). Чтобы запросить сертификат, установите флаг **сслрекуирецерт** . Для тестирования можно также задать эти параметры в IIS Express в локальном узле ApplicationHost. Файл конфигурации, расположенный в папке "Документс\иисекспресс\конфиг".

### <a name="creating-a-client-certificate-for-testing"></a>Создание сертификата клиента для тестирования

Для целей тестирования можно использовать [Makecert. exe](/windows/desktop/SecCrypto/makecert) для создания сертификата клиента. Сначала создайте тестовый корневой центр.

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

MakeCert предложит ввести пароль для закрытого ключа.

Затем добавьте сертификат в хранилище "Доверенные корневые центры сертификации" тестового сервера следующим образом:

1. Откройте MMC.
2. В разделе **файл**выберите **Добавить или удалить оснастку**.
3. Выберите **учетная запись компьютера**.
4. Выберите **локальный компьютер** и завершите работу мастера.
5. В области навигации разверните узел "Доверенные корневые центры сертификации".
6. В меню **действие** укажите **все задачи**, а затем нажмите кнопку **Импорт** , чтобы запустить мастер импорта сертификатов.
7. Перейдите к файлу сертификата TempCA. cer.
8. Нажмите кнопку **Открыть**, затем нажмите кнопку **Далее** и завершите работу мастера. (Вам будет предложено повторно ввести пароль.)

Теперь создайте сертификат клиента, подписанный первым сертификатом:

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a>Использование клиентских сертификатов в веб-API

На стороне сервера можно получить сертификат клиента, вызвав [жетклиентцертификате](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) в сообщении запроса. Метод возвращает значение null, если сертификат клиента отсутствует. В противном случае возвращается экземпляр **X509Certificate2** . Используйте этот объект для получения сведений из сертификата, например издателя и субъекта. Затем эти сведения можно использовать для проверки подлинности и (или) авторизации.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
