---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: начало работы с OWIN и Katana | Документация Майкрософт
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472446"
---
# <a name="getting-started-with-owin-and-katana"></a>Начало работы с OWIN и Katana

по [Майк Уоссон](https://github.com/MikeWasson)

[Открытый веб-интерфейс для .NET (OWIN)](http://owin.org/) определяет абстракцию между веб-серверами и веб-приложениями .NET. Отделив веб-сервер от приложения, OWIN упрощает создание по промежуточного слоя для разработки веб-приложений .NET. Кроме того, OWIN упрощает перенос веб-приложений на другие узлы&#8212;, например для размещения в службе Windows или в другом процессе.

OWIN является спецификацией, принадлежащей сообществом, а не реализацией. Проект Katana — это набор компонентов OWIN с открытым исходным кодом, разработанный корпорацией Майкрософт. Общие сведения о OWIN и Katana см. [в обзоре проекта Katana](an-overview-of-project-katana.md). В этой статье я буду сразу перейти к коду, чтобы приступить к работе.

В этом руководстве используется [версия-кандидат Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566), но можно также использовать Visual Studio 2012. Некоторые шаги отличаются в Visual Studio 2012, о которых я расмечу ниже.

## <a name="host-owin-in-iis"></a>Размещение OWIN в IIS

В этом разделе мы будем размещать OWIN в IIS. Этот параметр обеспечивает гибкость и компонуемости конвейера OWIN вместе с развитым набором функций IIS. При использовании этого параметра приложение OWIN выполняется в конвейере запросов ASP.NET.

Сначала создайте новый проект веб-приложения ASP.NET. (В Visual Studio 2012 используйте тип проекта ASP.NET Empty веб-приложения.)

![](getting-started-with-owin-and-katana/_static/image1.png)

В диалоговом окне **Новый проект ASP.NET** выберите **пустой** шаблон.

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>Добавление пакетов NuGet

Затем добавьте необходимые пакеты NuGet. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем выберите **консоль диспетчера пакетов**. В окне консоли диспетчера пакетов введите следующую команду:

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>Добавление класса запуска

Затем добавьте класс запуска OWIN. В обозреватель решений щелкните правой кнопкой мыши проект и выберите **Добавить**, а затем выберите **новый элемент**. В диалоговом окне **Добавление нового элемента** выберите **класс запуска Owin**. Дополнительные сведения о настройке класса Startup см. в разделе [Обнаружение класса запуска OWIN](owin-startup-class-detection.md).

![](getting-started-with-owin-and-katana/_static/image4.png)

Добавьте в метод `Startup1.Configuration` следующий код:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

Этот код добавляет к конвейеру OWIN простую часть по промежуточного слоя, реализованную в виде функции, получающей экземпляр **Microsoft. OWIN. иовинконтекст** . Когда сервер получает HTTP-запрос, конвейер OWIN вызывает по промежуточного слоя. По промежуточного слоя задает тип содержимого для ответа и записывает текст ответа.

> [!NOTE]
> Шаблон класса Startup OWIN доступен в Visual Studio 2013. Если вы используете Visual Studio 2012, просто добавьте новый пустой класс с именем `Startup1`и вставьте в него следующий код:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>Запуск приложения

Нажмите клавишу F5, чтобы начать отладку. Visual Studio откроет окно браузера для `http://localhost:*port*/`. Страница должна выглядеть следующим образом:

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>OWIN с самостоятельным размещением в консольном приложении

Это приложение легко преобразовать из IIS, размещенного в собственном размещении, в пользовательском процессе. При размещении IIS службы IIS действуют как как HTTP-сервер, так и как процесс, в котором размещена служба. В собственном размещении приложение создает процесс и использует класс **HttpListener** в качестве HTTP-сервера.

Создайте новое консольное приложение в Visual Studio. В окне консоли диспетчера пакетов введите следующую команду:

`Install-Package Microsoft.Owin.SelfHost -Pre`

Добавьте класс `Startup1` из части 1 этого учебника в проект. Вам не нужно изменять этот класс.

Реализуйте метод `Main` приложения следующим образом.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

При запуске консольного приложения сервер начинает прослушивание `http://localhost:9000`. При переходе по этому адресу в веб-браузере отображается страница "Hello World".

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>Добавить диагностику OWIN

Пакет Microsoft. Owin. Diagnostics содержит по промежуточного слоя, которое перехватывает необработанные исключения и отображает HTML-страницу со сведениями об ошибке. Эта страница работает примерно так же, как страница ошибок ASP.NET, которая иногда называется «[желтым экраном смерти](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)» (исод). Как и ИСОД, страница ошибки Katana полезна во время разработки, но ее рекомендуется отключить в рабочем режиме.

Чтобы установить пакет диагностики в проекте, введите в окне консоли диспетчера пакетов следующую команду:

`install-package Microsoft.Owin.Diagnostics –Pre`

Измените код в методе `Startup1.Configuration` следующим образом:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

Теперь используйте сочетание клавиш CTRL + F5 для запуска приложения без отладки, чтобы Visual Studio не нарушала исключение. Приложение ведет себя так же, как и раньше, пока вы не перейдите к `http://localhost/fail`, после чего приложение создаст исключение. По промежуточного слоя страницы ошибки будет перехватывать исключение и отображать HTML-страницу со сведениями об ошибке. Можно щелкнуть вкладки, чтобы просмотреть стек, строку запроса, файлы cookie, заголовок запроса и переменные среды OWIN.

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>Next Steps

- [Определение класса запуска OWIN](owin-startup-class-detection.md)
- [Использование OWIN для самостоятельного размещения веб-API ASP.NET](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [Использование OWIN для самостоятельного размещения SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
