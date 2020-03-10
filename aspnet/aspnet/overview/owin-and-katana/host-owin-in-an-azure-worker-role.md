---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Размещение OWIN в рабочей роли Azure | Документация Майкрософт
author: MikeWasson
description: В этом руководстве показано, как самостоятельно размещать OWIN в рабочей роли Microsoft Azure. Открытый веб-интерфейс для .NET (OWIN) определяет абстракцию между веб-сервером .NET...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472398"
---
# <a name="host-owin-in-an-azure-worker-role"></a>Размещение OWIN в рабочей роли Azure

по [Майк Уоссон](https://github.com/MikeWasson)

> В этом руководстве показано, как самостоятельно размещать OWIN в рабочей роли Microsoft Azure.
>
> [Открытый веб-интерфейс для .NET](http://owin.org/) (OWIN) определяет абстракцию между веб-серверами и веб-приложениями .NET. OWIN отделяет веб-приложение от сервера, что делает OWIN идеальным для самостоятельного размещения веб-приложения в собственном процессе вне служб IIS, например в рабочей роли Azure.
>
> В этом руководстве вы узнаете, как самостоятельно размещать приложения OWIN в рабочей роли Microsoft Azure. Дополнительные сведения о рабочих ролях см. в статье [модели выполнения Azure](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Версии программного обеспечения, используемые в этом руководстве
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [Пакет Azure SDK для .NET 2,3](https://azure.microsoft.com/downloads/)
> - [Microsoft. Owin. резидент 2.1.0](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a>Создание проекта Microsoft Azure

Запустите Visual Studio с правами администратора. Права администратора необходимы для локальной отладки приложения с помощью эмулятора вычислений Azure.

В меню **файл** выберите пункт **создать**, а затем выберите пункт **проект**. На странице **Установленные шаблоны**в разделе C#визуальный элемент щелкните **облако** , а затем щелкните **облачная служба Windows Azure**. Присвойте проекту имя "AzureApp" и нажмите кнопку **ОК**.

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

В диалоговом окне **новая облачная служба Windows Azure** дважды щелкните **Рабочая роль**. Оставьте имя по умолчанию ("WorkerRole1"). На этом шаге Рабочая роль добавляется в решение. Нажмите кнопку **ОК**.

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

Созданное решение Visual Studio содержит два проекта:

- &quot;AzureApp&quot; определяет роли и конфигурацию для приложения Azure.
- &quot;WorkerRole1&quot; содержит код для рабочей роли.

Как правило, приложение Azure может содержать несколько ролей, хотя в этом учебнике используется одна роль.

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a>Добавление пакетов с самостоятельным размещением OWIN

В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем щелкните **консоль диспетчера пакетов**.

В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>Добавление конечной точки HTTP

В обозреватель решений разверните проект AzureApp. Разверните узел роли, щелкните правой кнопкой мыши WorkerRole1 и выберите пункт **Свойства**.

![](host-owin-in-an-azure-worker-role/_static/image6.png)

Выберите **Конечные точки** и нажмите кнопку **Добавить конечную точку**.

В раскрывающемся списке **протокол** выберите "http". В окне **Общий порт** и **частный порт**введите 80. Эти номера портов могут отличаться. Общедоступный порт используется клиентами при отправке запроса роли.

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a>Создание класса запуска OWIN

В обозреватель решений щелкните правой кнопкой мыши проект WorkerRole1 и выберите **добавить** / **класс** , чтобы добавить новый класс. Назовите класс `Startup`.

Замените весь стандартный код следующим:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

Метод расширения `UseWelcomePage` добавляет в приложение простую HTML-страницу, чтобы убедиться, что сайт работает.

## <a name="start-the-owin-host"></a>Запуск узла OWIN

Откройте файл WorkerRole.cs. Этот класс определяет код, который выполняется при запуске и остановке рабочей роли.

Добавьте следующую инструкцию using:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

Добавьте элемент **IDisposable** в класс `WorkerRole`:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

В методе `OnStart` добавьте следующий код для запуска узла:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

Метод **webapp. Start** запускает узел OWIN. Имя класса `Startup` является параметром типа для метода. По соглашению узел будет вызывать метод `Configure` этого класса.

Переопределите `OnStop`, чтобы освободить экземпляр *\_ного приложения* :

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

Ниже приведен полный код для WorkerRole.cs:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

Выполните сборку решения и нажмите клавишу F5, чтобы запустить приложение локально в эмуляторе вычислений Azure. В зависимости от параметров брандмауэра может потребоваться разрешить эмулятор через брандмауэр.

Эмулятор вычислений назначает конечной точке локальный IP-адрес. IP-адрес можно найти, просмотрев пользовательский интерфейс эмулятора вычислений. Щелкните правой кнопкой мыши значок эмулятора в области уведомлений панели задач и выберите пункт **отобразить пользовательский интерфейс эмулятора вычислений**.

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

Найдите IP-адрес в разделе развертывания службы, развертывание [ИД], сведения о службе. Откройте веб-браузер и перейдите по *адресу*http:\/\/Address, где *Address* — это IP-адрес, назначенный эмулятором вычислений. Например, `http://127.0.0.1:80`. Вы должны увидеть страницу приветствия OWIN:

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a>Развертывание в Azure

Для этого шага необходимо иметь учетную запись Azure. Если у вас ее еще нет, вы можете создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье [Microsoft Azure Бесплатная пробная версия](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).

В обозреватель решений щелкните правой кнопкой мыши проект AzureApp. Нажмите кнопку **Опубликовать**.

![](host-owin-in-an-azure-worker-role/_static/image12.png)

Если вы не вошли в учетную запись Azure, щелкните **войти**.

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

После входа выберите подписку и нажмите кнопку **Далее**.

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

Введите имя для облачной службы и выберите регион. Нажмите кнопку **Создать**.

![](host-owin-in-an-azure-worker-role/_static/image17.png)

Щелкните **Опубликовать**.

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

В окне Журнал действий Azure отображается ход развертывания. При развертывании приложения перейдите к `http://appname.cloudapp.net/`, где *AppName* — это имя вашей облачной службы.

## <a name="additional-resources"></a>Дополнительные ресурсы

- [Обзор проекта Katana](an-overview-of-project-katana.md)
- [Проект Katana на GitHub](https://github.com/aspnet/AspNetKatana/)
