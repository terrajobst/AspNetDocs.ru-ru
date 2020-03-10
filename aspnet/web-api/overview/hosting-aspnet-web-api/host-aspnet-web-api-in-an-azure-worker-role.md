---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Размещение веб-API ASP.NET 2 в рабочей роли Azure — ASP.NET 4. x
author: MikeWasson
description: Руководство. размещение веб-API ASP.NET в рабочей роли Azure с помощью OWIN для самостоятельного размещения платформы веб-API.
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448410"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a>Размещение веб-API ASP.NET 2 в рабочей роли Azure

по [Майк Уоссон](https://github.com/MikeWasson)

> В этом руководстве показано, как разместить веб-API ASP.NET в рабочей роли Azure с помощью OWIN для самостоятельного размещения платформы веб-API.
>
> [Открытый веб-интерфейс для .NET](http://owin.org/) (OWIN) определяет абстракцию между веб-серверами и веб-приложениями .NET. OWIN отделяет веб-приложение от сервера, что делает OWIN идеальным для самостоятельного размещения веб-приложения в собственном процессе вне служб IIS, например в рабочей роли Azure.
>
> В этом руководстве вы будете использовать пакет Microsoft. Owin. host. HttpListener, который предоставляет HTTP-сервер, используемый для самостоятельного размещения приложений OWIN.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Веб-API 2
> - [Пакет Azure SDK для .NET 2,3](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a>Создание проекта Microsoft Azure

Запустите Visual Studio с правами администратора. Права администратора необходимы для локальной отладки приложения с помощью эмулятора вычислений Azure.

В меню **файл** выберите пункт **создать**, а затем выберите пункт **проект**. На странице **Установленные шаблоны**в разделе C#визуальный элемент щелкните **облако** , а затем щелкните **облачная служба Windows Azure**. Присвойте проекту имя "AzureApp" и нажмите кнопку **ОК**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

В диалоговом окне **новая облачная служба Windows Azure** дважды щелкните **Рабочая роль**. Оставьте имя по умолчанию ("WorkerRole1"). На этом шаге Рабочая роль добавляется в решение. Нажмите кнопку **ОК**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

Созданное решение Visual Studio содержит два проекта:

- &quot;AzureApp&quot; определяет роли и конфигурацию для приложения Azure.
- &quot;WorkerRole1&quot; содержит код для рабочей роли.

Как правило, приложение Azure может содержать несколько ролей, хотя в этом учебнике используется одна роль.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a>Добавление веб-API и пакетов OWIN

В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем щелкните **консоль диспетчера пакетов**.

В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>Добавление конечной точки HTTP

В обозреватель решений разверните проект AzureApp. Разверните узел роли, щелкните правой кнопкой мыши WorkerRole1 и выберите пункт **Свойства**.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

Выберите **Конечные точки** и нажмите кнопку **Добавить конечную точку**.

В раскрывающемся списке **протокол** выберите "http". В окне **Общий порт** и **частный порт**введите 80. Эти номера портов могут отличаться. Общедоступный порт используется клиентами при отправке запроса роли.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a>Настройка веб-API для самостоятельного размещения

В обозреватель решений щелкните правой кнопкой мыши проект WorkerRole1 и выберите **добавить** / **класс** , чтобы добавить новый класс. Назовите класс `Startup`.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

Замените весь стандартный код в этом файле следующим кодом:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a>Добавление контроллера веб-API

Затем добавьте класс контроллера веб-API. Щелкните правой кнопкой мыши проект WorkerRole1 и выберите **Добавить** **класс** / . Назовите класс TestController. Замените весь стандартный код в этом файле следующим кодом:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

Для простоты этот контроллер просто определяет два метода GET, которые возвращают обычный текст.

## <a name="start-the-owin-host"></a>Запуск узла OWIN

Откройте файл WorkerRole.cs. Этот класс определяет код, который выполняется при запуске и остановке рабочей роли.

Добавьте следующую инструкцию using:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

Добавьте элемент **IDisposable** в класс `WorkerRole`:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

В методе `OnStart` добавьте следующий код для запуска узла:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

Метод **webapp. Start** запускает узел OWIN. Имя класса `Startup` является параметром типа для метода. По соглашению узел будет вызывать метод `Configure` этого класса.

Переопределите `OnStop`, чтобы освободить экземпляр *\_ного приложения* :

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

Ниже приведен полный код для WorkerRole.cs:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

Выполните сборку решения и нажмите клавишу F5, чтобы запустить приложение локально в эмуляторе вычислений Azure. В зависимости от параметров брандмауэра может потребоваться разрешить эмулятор через брандмауэр.

> [!NOTE]
> Если вы получаете исключение, аналогичное приведенному ниже, ознакомьтесь с [этой записью в блоге](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) для решения этой проблемы. «Не удалось загрузить файл или сборку Microsoft. Owin, Version = 2.0.2.0, Culture = Neutral, PublicKeyToken = 31bf3856ad364e35» или одну из ее зависимостей. Определение манифеста найденной сборки не соответствует ссылке на сборку. (Исключение из HRESULT: 0x80131040) "

Эмулятор вычислений назначает конечной точке локальный IP-адрес. IP-адрес можно найти, просмотрев пользовательский интерфейс эмулятора вычислений. Щелкните правой кнопкой мыши значок эмулятора в области уведомлений панели задач и выберите пункт **отобразить пользовательский интерфейс эмулятора вычислений**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

Найдите IP-адрес в разделе развертывания службы, развертывание [ИД], сведения о службе. Откройте веб-браузер и перейдите по<em>адресу http://Address</em>/Test/1, где <em>Address</em> — это IP-адрес, назначенный эмулятором вычислений. Например, `http://127.0.0.1:80/test/1`. Вы должны увидеть ответ от контроллера веб-API:

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a>Развертывание в Azure

Для этого шага необходимо иметь учетную запись Azure. Если у вас ее еще нет, вы можете создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье [Microsoft Azure Бесплатная пробная версия](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).

В обозреватель решений щелкните правой кнопкой мыши проект AzureApp. Нажмите кнопку **Опубликовать**.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

Если вы не вошли в учетную запись Azure, щелкните **войти**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

После входа выберите подписку и нажмите кнопку **Далее**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

Введите имя для облачной службы и выберите регион. Нажмите кнопку **Создать**.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

Щелкните **Опубликовать**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

В окне Журнал действий Azure отображается ход развертывания. При развертывании приложения перейдите к http://appname.cloudapp.net/test/1.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Обзор проекта Katana](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [Проект Katana на GitHub](https://github.com/aspnet/AspNetKatana)
