---
uid: web-api/overview/security/external-authentication-services
title: Внешние службы проверки подлинностиC#с веб-API ASP.NET () | Документация Майкрософт
author: rmcmurray
description: Описание использования внешних служб проверки подлинности в веб-API ASP.NET.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447420"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a>Внешние службы проверки подлинностиC#с веб-API ASP.NET ()

Visual Studio 2017 и ASP.NET 4.7.2 расширяют возможности безопасности для [одностраничных приложений](../../../single-page-application/index.md) (SPA) и служб [веб-API](../../index.md) для интеграции с внешними службами проверки подлинности, включая несколько служб OAuth/OpenID Connect и службы проверки подлинности социальных сетей: учетные записи Майкрософт, Twitter, Facebook и Google.  

### <a name="in-this-walkthrough"></a>В этом пошаговом руководстве

- [Использование внешних служб проверки подлинности](#USING)
- [Создание примера веб-приложения](#SAMPLE)
- [Включение проверки подлинности Facebook](#FACEBOOK)
- [Включение проверки подлинности Google](#GOOGLE)
- [Включение проверки подлинности Майкрософт](#MICROSOFT)
- [Включение проверки подлинности Twitter](#TWITTER)
- [Дополнительная информация](#MOREINFO)

    - [Объединение внешних служб проверки подлинности](#COMBINE)
    - [Настройка IIS Express для использования полного доменного имени](#FQDN)
    - [Как получить параметры приложения для проверки подлинности Майкрософт](#OBTAIN)
    - [Необязательно: отключить локальную регистрацию](#DISABLE)

### <a name="prerequisites"></a>предварительные требования

Для выполнения примеров в этом пошаговом руководстве необходимо следующее:

- Visual Studio 2017
- Учетная запись разработчика с идентификатором приложения и секретным ключом для одной из следующих служб проверки подлинности социальных сетей:

  - Учетные записи Майкрософт ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))
  - Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))
  - Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))
  - Google ([https://developers.google.com/](https://developers.google.com))

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>Использование внешних служб проверки подлинности

Множество внешних служб проверки подлинности, которые в настоящее время доступны веб-разработчикам, помогают сократить время разработки для создания новых веб-приложений. Веб-пользователи обычно имеют несколько существующих учетных записей для популярных веб-служб и веб-сайтов социальных сетей, поэтому, когда веб-приложение реализует службы проверки подлинности из внешней веб-службы или веб-сайта социальных сетей, оно сохраняет время разработки, которое было бы затрачено на создание реализации проверки подлинности. Использование внешней службы проверки подлинности экономит пользователей от необходимости создавать другую учетную запись для веб-приложения, а также от необходимости запоминать другое имя пользователя и пароль.

В прошлом разработчики имели два варианта: создать собственную реализацию проверки подлинности или изучить интеграцию внешней службы проверки подлинности в свои приложения. На схеме ниже показан простой поток запросов для агента пользователя (веб-браузера), запрашивающего информацию из веб-приложения, которое настроено для использования внешней службы проверки подлинности.

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

На предыдущей схеме агент пользователя (или веб-браузер в этом примере) выполняет запрос к веб-приложению, которое перенаправляет веб-браузер на внешнюю службу проверки подлинности. Агент пользователя отправляет свои учетные данные внешней службе проверки подлинности, и если агент пользователя успешно прошел проверку подлинности, внешняя служба проверки подлинности перенаправит агент пользователя в исходное веб-приложение с помощью некоторого маркера, который агент пользователя будет передавать в веб-приложение. Веб-приложение будет использовать маркер, чтобы убедиться, что агент пользователя успешно прошел проверку подлинности с помощью внешней службы проверки подлинности, а веб-приложение может использовать маркер для сбора дополнительных сведений об агенте пользователя. После того, как приложение завершит обработку данных агента пользователя, веб-приложение вернет соответствующий ответ агенту пользователя на основе его параметров авторизации.

Во втором примере агент пользователя согласовывает с веб-приложением и внешним сервером авторизации, а веб-приложение выполняет дополнительное взаимодействие с внешним сервером авторизации для получения дополнительных сведений о пользователе. Субагент

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

Visual Studio 2017 и ASP.NET 4.7.2 упрощают интеграцию с внешними службами аутентификации для разработчиков, предоставляя встроенную интеграцию для следующих служб проверки подлинности:

- Facebook
- Google
- Учетные записи Майкрософт (учетные записи Windows Live ID)
- Twitter

В примерах этого пошагового руководства будет продемонстрировано, как настроить каждую из поддерживаемых внешних служб проверки подлинности с помощью нового шаблона веб-приложения ASP.NET, поставляемого с Visual Studio 2017.

> [!NOTE]
> При необходимости может потребоваться добавить полное доменное имя в параметры внешней службы проверки подлинности. Это требование основано на ограничениях безопасности для некоторых внешних служб аутентификации, которым требуется полное доменное имя в параметрах приложения, чтобы соответствовать полному доменному имени, используемому клиентами. (Шаги для этого будут сильно различаться для каждой внешней службы проверки подлинности. для каждой внешней службы проверки подлинности необходимо обратиться к документации, чтобы узнать, является ли это обязательным и как настроить эти параметры.) Если необходимо настроить IIS Express для использования полного доменного имени для тестирования этой среды, см. раздел [настройка IIS Express для использования полного доменного имен](#FQDN) далее в этом пошаговом руководстве.

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a>Создание примера веб-приложения

Следующие шаги помогут вам создать пример приложения с помощью шаблона веб-приложения ASP.NET. Этот пример приложения будет использоваться для каждой из внешних служб проверки подлинности далее в этом пошаговом руководстве.

Запустите Visual Studio 2017 и выберите **создать проект** на начальной странице. Либо в меню **файл** выберите **создать** , а затем — **проект**.

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

Когда откроется диалоговое окно **Создание проекта** , выберите **установлено** и разверните элемент **Visual C#** . В **разделе C#визуальный** элемент выберите **веб**. В списке шаблонов проектов выберите **ASP.NET веб-приложение (.NET Framework)** . Введите имя проекта и нажмите кнопку **ОК**.

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

Когда отобразится **Новый проект ASP.NET** , выберите шаблон **одностраничное приложение** и нажмите кнопку **создать проект**.

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

Подождите, пока Visual Studio 2017 создаст проект.

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

Когда Visual Studio 2017 завершит создание проекта, откройте файл *Startup.auth.CS* , расположенный в папке **app\_Start** .

При первом создании проекта ни одна из внешних служб проверки подлинности не включена в файл *Startup.auth.CS* ; Ниже показано, что может напоминать код, и разделы, выделенные для того, чтобы включить внешнюю службу проверки подлинности и соответствующие параметры для использования учетных записей Майкрософт, Twitter, Facebook или Google в приложении ASP.NET:

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

При нажатии клавиши F5 для сборки и отладки веб-приложения отображается экран входа в систему, где вы увидите, что внешние службы проверки подлинности не определены.

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

В следующих разделах вы узнаете, как включить каждую из внешних служб проверки подлинности, предоставляемых с ASP.NET в Visual Studio 2017.

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>Включение проверки подлинности Facebook

При использовании проверки подлинности Facebook необходимо создать учетную запись разработчика Facebook, а для работы проекта потребуется идентификатор приложения и секретный ключ из Facebook. Сведения о создании учетной записи разработчика Facebook и получении идентификатора приложения и секретного ключа см. в разделе [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).

Получив идентификатор приложения и секретный ключ, выполните следующие действия, чтобы включить проверку подлинности Facebook для веб-приложения.

1. Когда проект откроется в Visual Studio 2017, откройте файл *Startup.auth.CS* .

2. Откройте раздел кода проверки подлинности Facebook:

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. Удалите &quot;//&quot; символы, чтобы раскомментировать выделенные строки кода, а затем добавьте идентификатор приложения и секретный ключ. После добавления этих параметров можно выполнить повторную компиляцию проекта:

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. При нажатии клавиши F5 для открытия веб-приложения в веб-браузере вы увидите, что Facebook определен как внешняя служба проверки подлинности:

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. При нажатии кнопки **Facebook** браузер будет перенаправлен на страницу входа Facebook:

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. После ввода учетных данных Facebook и нажатия кнопки **войти**ваш веб-браузер перенаправится обратно в веб-приложение, в котором будет предложено ввести **имя пользователя** , которое нужно связать с учетной записью Facebook:

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. После того как вы введете имя пользователя и настроили кнопку **Регистрация** , веб-приложение отобразит **домашнюю страницу** по умолчанию для учетной записи Facebook:

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>Включение проверки подлинности Google

Для использования проверки подлинности Google необходимо создать учетную запись разработчика Google, а для работы с вашим проектом потребуется идентификатор приложения и секретный ключ из Google. Сведения о создании учетной записи разработчика Google и получении идентификатора приложения и секретного ключа см. в разделе [https://developers.google.com](https://developers.google.com).

Чтобы включить проверку подлинности Google для веб-приложения, выполните следующие действия.

1. Когда проект откроется в Visual Studio 2017, откройте файл *Startup.auth.CS* .

2. Откройте раздел кода для проверки подлинности Google:

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. Удалите &quot;//&quot; символы, чтобы раскомментировать выделенные строки кода, а затем добавьте идентификатор приложения и секретный ключ. После добавления этих параметров можно выполнить повторную компиляцию проекта:

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. При нажатии клавиши F5 для открытия веб-приложения в веб-браузере вы увидите, что Google был определен как внешняя служба проверки подлинности:

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. При нажатии кнопки **Google** браузер будет перенаправлен на страницу входа в Google:

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. После ввода учетных данных Google и нажатия кнопки **войти в**Google появится запрос на подтверждение наличия у веб-приложения разрешений на доступ к учетной записи Google.

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. При нажатии кнопки **принять**веб-браузер перенаправится обратно в веб-приложение, в котором будет предложено ввести **имя пользователя** , которое нужно связать с учетной записью Google.

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. После того как вы введете имя пользователя и настроили кнопку **Регистрация** , веб-приложение отобразит **домашнюю страницу** по умолчанию для вашей учетной записи Google:

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>Включение проверки подлинности Майкрософт

Проверка подлинности Майкрософт требует создания учетной записи разработчика, для работы которой требуется идентификатор клиента и секрет клиента. Сведения о создании учетной записи разработчика Майкрософт и получении идентификатора клиента и секрета клиента см. в разделе [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).

После получения ключа и секрета потребителя выполните следующие действия, чтобы включить проверку подлинности Майкрософт для веб-приложения.

1. Когда проект откроется в Visual Studio 2017, откройте файл *Startup.auth.CS* .

2. Откройте раздел кода проверки подлинности Майкрософт:

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. Удалите &quot;//&quot; символы, чтобы раскомментировать выделенные строки кода, а затем добавьте идентификатор клиента и секрет клиента. После добавления этих параметров можно выполнить повторную компиляцию проекта:

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. При нажатии клавиши F5 для открытия веб-приложения в веб-браузере вы увидите, что Microsoft определено как внешняя служба проверки подлинности:

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. При нажатии кнопки " **Microsoft** " браузер будет перенаправлен на страницу входа Майкрософт:

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. После ввода учетных данных Майкрософт и нажатия кнопки **войти**вам будет предложено проверить наличие у веб-приложения разрешений на доступ к учетная запись Майкрософт:

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. При нажатии кнопки **"Да"** веб-браузер будет перенаправлен обратно в веб-приложение, в котором будет предложено ввести **имя пользователя** , которое нужно связать с учетная запись Майкрософт:

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. После того как вы введете имя пользователя и настроили кнопку **Регистрация** , веб-приложение отобразит **домашнюю страницу** по умолчанию для учетная запись Майкрософт:

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>Включение проверки подлинности Twitter

Для проверки подлинности в Twitter необходимо создать учетную запись разработчика, а для ее работы требуется ключ потребителя и секрет клиента. Сведения о создании учетной записи разработчика Twitter и получении ключа потребителя и секрета потребителя см. в разделе [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).

После получения ключа и секрета потребителя выполните следующие действия, чтобы включить проверку подлинности Twitter для веб-приложения.

1. Когда проект откроется в Visual Studio 2017, откройте файл *Startup.auth.CS* .

2. Откройте раздел кода проверки подлинности Twitter:

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. Удалите &quot;//&quot; символы, чтобы раскомментировать выделенные строки кода, а затем добавьте ключ потребителя и секрет потребителя. После добавления этих параметров можно выполнить повторную компиляцию проекта:

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. При нажатии клавиши F5 для открытия веб-приложения в веб-браузере вы увидите, что Twitter был определен как внешняя служба проверки подлинности:

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. При нажатии кнопки **Twitter** браузер будет перенаправлен на страницу входа Twitter:

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. После ввода учетных данных Twitter и нажатия кнопки **авторизовать приложение**веб-браузер будет перенаправлен обратно в веб-приложение, в котором будет предложено ввести **имя пользователя** , которое нужно связать с учетной записью Twitter:

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. После того как вы введете имя пользователя и настроили кнопку **Регистрация** , в веб-приложении отобразится **Домашняя страница** по умолчанию для учетной записи Twitter:

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>Дополнительные сведения

Дополнительные сведения о создании приложений, использующих OAuth и OpenID Connect, см. по следующим URL-адресам:

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>Объединение внешних служб проверки подлинности

Для большей гибкости можно одновременно определить несколько внешних служб проверки подлинности. Это позволит пользователям веб-приложения использовать учетную запись из любой включенной внешней службы проверки подлинности.

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a>Настройка IIS Express для использования полного доменного имени

Некоторые внешние поставщики проверки подлинности не поддерживают тестирование приложения с помощью HTTP-адреса, например `http://localhost:port/`. Чтобы обойти эту ошибку, можно добавить в файл HOSTs статическое сопоставление полного доменного имени (FQDN) и настроить параметры проекта в Visual Studio 2017 для использования полного доменного имени для тестирования и отладки. Для этого выполните следующие действия.

- Добавьте статическое полное доменное имя, сопоставленное с файлом HOSTs:

  1. Откройте командную строку с повышенными привилегиями в Windows.
  2. Введите следующую команду:

      <kbd>Блокнот,%WinDir%\system32\drivers\etc\hosts</kbd>
  3. Добавьте запись, подобную приведенной ниже, в файл HOSTs:

      <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
  4. Сохраните и закройте файл HOSTs.

- Настройте проект Visual Studio для использования полного доменного имени:

  1. Когда проект откроется в Visual Studio 2017, откройте меню **проект** и выберите Свойства проекта. Например, можно выбрать **Свойства WebApplication1**.
  2. Перейдите на вкладку **веб** .
  3. Введите полное доменное имя для <strong>URL-адреса проекта</strong>. Например, можно ввести <kbd><http://www.wingtiptoys.com></kbd> , если это сопоставление FQDN, добавленное в файл hosts.

- Настройте IIS Express для использования полного доменного имени приложения:

    1. Откройте командную строку с повышенными привилегиями в Windows.
    2. Введите следующую команду, чтобы перейти к папке IIS Express:

        <kbd>CD/d &quot;%Програмфилес%\иис Express&quot;</kbd>
    3. Введите следующую команду, чтобы добавить полное доменное имя в приложение:

        <kbd>Appcmd. exe set config-Section: System. applicationHost/Sites/+&quot;[имя = ' WebApplication1 ']. Bindings. [Protocol = ' http ', bindingInformation = ' *: 80: www. wingtiptoys. com ']&quot;/commit: APPHOST</kbd>

  Где **WebApplication1** — имя вашего проекта, а **bindingInformation** содержит номер порта и полное доменное имя, которое вы хотите использовать для тестирования.

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>Как получить параметры приложения для проверки подлинности Майкрософт

Связывание приложения с Windows Live для проверки подлинности Майкрософт — это простой процесс. Если вы еще не связали приложение с Windows Live, можно выполнить следующие действия.

1. Перейдите к [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) и введите имя учетная запись Майкрософт и пароль при появлении запроса, а затем щелкните **войти**:

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. Выберите **Добавить приложение** и введите имя приложения при появлении запроса, а затем нажмите кнопку **создать**.

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. Выберите свое приложение в списке **имя** и свойства его приложения.

4. Введите домен перенаправления для приложения. Скопируйте **идентификатор приложения** и в разделе **секреты приложения**выберите **создать пароль**. Скопируйте отображаемый пароль. ИДЕНТИФИКАТОР и пароль приложения являются ИДЕНТИФИКАТОРом клиента и секретом клиента. Нажмите кнопку **ОК** , а затем **сохранить**.

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>Необязательно: отключить локальную регистрацию

Текущая функция локальной регистрации ASP.NET не мешает автоматическим программам (программы-роботы) создавать учетные записи членов. Например, с помощью технологии «Bot-предотвращение» и проверки, такой как [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md). Поэтому на странице входа необходимо удалить локальную форму входа и ссылку регистрации. Для этого откройте страницу *\_Login. cshtml* в проекте, а затем закомментируйте строки для локальной панели входа и регистрационной ссылки. Полученная страница должна выглядеть, как в следующем примере кода:

[!code-html[Main](external-authentication-services/samples/sample10.html)]

После отключения локальной панели входа и ссылки регистрации на странице входа будут отображаться только внешние поставщики проверки подлинности, которые были включены.

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
