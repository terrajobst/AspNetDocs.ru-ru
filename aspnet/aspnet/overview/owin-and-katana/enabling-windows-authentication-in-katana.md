---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Включение проверки подлинности Windows в Katana | Документация Майкрософт
author: MikeWasson
description: 'В этой статье показано, как включить проверку подлинности Windows в Katana. В нем рассматриваются два сценария: Использование IIS для размещения Katana и использование HttpListener для самостоятельного размещения Kat...'
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500298"
---
# <a name="enabling-windows-authentication-in-katana"></a>Включение проверки подлинности Windows в Katana

по [Майк Уоссон](https://github.com/MikeWasson)

> В этой статье показано, как включить проверку подлинности Windows в Katana. В нем рассматриваются два сценария: Использование IIS для размещения Katana и использование HttpListener для самостоятельного размещения Katana в пользовательском процессе. Спасибо Барри Доррансом, Дэвид Матсон и Крис Росс (для ознакомления с этой статьей.

Katana — это реализация [OWIN](http://owin.org/)Майкрософт с открытым веб-интерфейсом для .NET. Вы можете ознакомиться с введением в OWIN и Katana [здесь](an-overview-of-project-katana.md). Архитектура OWIN имеет несколько уровней:

- Узел. управляет процессом, в котором выполняется конвейер OWIN.
- Сервер: открывает сетевой сокет и прослушивает запросы.
- По промежуточного слоя: обрабатывает HTTP-запрос и ответ.

В настоящее время Katana предоставляет два сервера, оба из которых поддерживают встроенную проверку подлинности Windows:

- **Microsoft. Owin. host. SystemWeb**. Использует службы IIS с конвейером ASP.NET.
- **Microsoft. Owin. host. HttpListener**. Использует [System .NET. HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx). Этот сервер в настоящее время является параметром по умолчанию при размещении в собственном расположении Katana.

> [!NOTE]
> Katana в настоящее время не предоставляет по промежуточного слоя OWIN для проверки подлинности Windows, так как эта функция уже доступна на серверах.

## <a name="windows-authentication-in-iis"></a>Проверка подлинности Windows в IIS

С помощью Microsoft. Owin. host. SystemWeb можно просто включить проверку подлинности Windows в службах IIS.

Начнем с создания нового приложения ASP.NET с помощью шаблона проекта "ASP.NET Empty веб-приложение".

![](enabling-windows-authentication-in-katana/_static/image1.png)

Затем добавьте пакеты NuGet. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

Теперь добавьте класс с именем `Startup` со следующим кодом:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

Это все, что необходимо для создания приложения "Hello World" для OWIN, работающего на IIS. Нажмите клавишу F5, чтобы начать отладку приложения. Вы должны увидеть текст "Hello World!" в окне браузера.

![](enabling-windows-authentication-in-katana/_static/image2.png)

Далее мы будем включать проверку подлинности Windows в IIS Express. В меню **вид** выберите пункт **свойства**. Щелкните имя проекта в обозреватель решений, чтобы просмотреть свойства проекта.

В окне **Свойства** задайте для параметра **Анонимная проверка подлинности** значение **отключено** и установите для параметра **Проверка подлинности Windows** значение **включено**.

![](enabling-windows-authentication-in-katana/_static/image3.png)

При запуске приложения из Visual Studio IIS Express потребуется учетные данные пользователя Windows. Это можно увидеть с помощью [Fiddler](http://fiddler2.com/home) или другого средства отладки HTTP. Ниже приведен пример HTTP-ответа.

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

Заголовки WWW-Authenticate в этом ответе указывают, что сервер поддерживает протокол [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) , использующий Kerberos или NTLM.

Затем при развертывании приложения на сервере выполните следующие [действия](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) , чтобы включить проверку подлинности Windows в службах IIS на этом сервере.

## <a name="windows-authentication-in-httplistener"></a>Проверка подлинности Windows в HttpListener

Если вы используете Microsoft. Owin. host. HttpListener для самостоятельного размещения Katana, вы можете включить проверку подлинности Windows непосредственно в экземпляре **HttpListener** .

Сначала создайте консольное приложение. Затем добавьте пакеты NuGet. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне "Консоль диспетчера пакетов" введите следующую команду:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

Теперь добавьте класс с именем `Startup` со следующим кодом:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

Этот класс реализует тот же самый пример "Hello World" из ранее, но также устанавливает проверку подлинности Windows в качестве схемы проверки подлинности.

В функции `Main` запустите конвейер OWIN:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

Вы можете отправить запрос в Fiddler, чтобы убедиться, что приложение использует проверку подлинности Windows:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>См. также

[Обзор проекта Katana](an-overview-of-project-katana.md)

[System.Net.HttpListener;](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[Основные сведения о проверке подлинности в OWIN Forms в MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
