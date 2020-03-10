---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: Обнаружение класса запуска OWIN | Документация Майкрософт
author: Praburaj
description: В этом руководстве показано, как настроить, какой класс запуска OWIN загружается. Дополнительные сведения о OWIN см. в обзоре проекта Katana. Этот учебник был...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500184"
---
# <a name="owin-startup-class-detection"></a>Определение класса запуска OWIN

> В этом руководстве показано, как настроить, какой класс запуска OWIN загружается. Дополнительные сведения о OWIN см. [в обзоре проекта Katana](an-overview-of-project-katana.md). Этот учебник написан на Рик Андерсон (( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), прабураж Сиагаражан и Говард дайеркинг ( [@howard\_Дайеркинг](https://twitter.com/howard_dierking) ).
>
> ## <a name="prerequisites"></a>предварительные требования
>
> [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a>Определение класса запуска OWIN

 Каждое приложение OWIN имеет класс Startup, в котором указываются компоненты для конвейера приложения. Существует несколько способов подключения класса Startup к среде выполнения в зависимости от выбранной модели размещения (Овинхост, IIS и IIS-Express). Класс Startup, показанный в этом учебнике, можно использовать во всех приложениях размещения. Вы подключаете класс Startup к среде выполнения размещения, используя один из следующих подходов:

1. **Соглашение об именовании**: Katana ищет класс с именем `Startup` в пространстве имен, соответствующем имени сборки или глобальному пространству имен.
2. **Атрибут овинстартуп**: это подход, который большинство разработчиков будет использовать для указания класса Startup. Следующий атрибут задает классу Startup классу `TestStartup` в пространстве имен `StartupDemo`.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   Атрибут `OwinStartup` переопределяет соглашение об именовании. Можно также указать понятное имя с помощью этого атрибута, однако при использовании понятного имени необходимо также использовать элемент `appSetting` в файле конфигурации.
3. **Элемент appSetting в файле конфигурации**: элемент `appSetting` переопределяет атрибут `OwinStartup` и соглашение об именовании. Можно использовать несколько классов запуска (каждый с помощью атрибута `OwinStartup`) и указать, какой класс запуска будет загружаться в файл конфигурации, используя разметку, аналогичную следующей:

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   Следующий ключ, явно указывающий класс запуска и сборку, также можно использовать:

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   Следующий XML-код в файле конфигурации указывает понятное имя класса запуска `ProductionConfiguration`.

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   Приведенная выше разметка должна использоваться со следующим атрибутом `OwinStartup`, который указывает понятное имя и приводит к запуску `ProductionStartup2` класса.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. Чтобы отключить обнаружение запуска OWIN, добавьте `appSetting owin:AutomaticAppStartup` со значением `"false"` в файле Web. config.

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>Создание веб-приложения ASP.NET с помощью OWIN Startup

1. Создайте пустое веб-приложение Asp.Net и назовите его **стартупдемо**. — Установите `Microsoft.Owin.Host.SystemWeb` с помощью диспетчера пакетов NuGet. В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем — **консоль диспетчера пакетов**. Введите следующую команду:

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. Добавьте класс запуска OWIN. В Visual Studio 2017 щелкните проект правой кнопкой мыши и выберите **Добавить класс**. — в диалоговом окне **Добавление нового элемента** введите *OWIN* в поле поиска и измените имя на Startup.cs, а затем нажмите кнопку **Добавить**.

     ![](owin-startup-class-detection/_static/image1.png)

   В следующий раз, когда нужно добавить *класс запуска Owin*, он будет доступен в меню **Добавить** .

     ![](owin-startup-class-detection/_static/image2.png)

   Кроме того, можно щелкнуть проект правой кнопкой мыши и выбрать **Добавить**, выбрать пункт **создать элемент**, а затем выбрать **класс запуска Owin**.

     ![](owin-startup-class-detection/_static/image3.png)

- Замените созданный код в файле *Startup.CS* следующим кодом:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  `app.Use` лямбда-выражение используется для регистрации указанного компонента по промежуточного слоя в конвейере OWIN. В этом случае мы настраиваете ведение журнала входящих запросов перед ответом на входящий запрос. Параметр `next` — это делегат ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt;) к следующему компоненту в конвейере. `app.Run` лямбда-выражение подключает конвейер к входящим запросам и предоставляет механизм ответа.
     > [!NOTE]
     > В приведенном выше коде мы добавили в комментарий атрибут `OwinStartup`, и мы используем соглашение о запуске класса с именем `Startup`. для запуска приложения нажмите клавишу ***F5*** . Несколько раз нажмите кнопку "Обновить".

    ![](owin-startup-class-detection/_static/image4.png) Примечание. число, показанное в изображениях этого учебника, не будет совпадать с отображаемым числом. Строка миллисекунды используется для отображения нового ответа при обновлении страницы.
  Данные трассировки можно просмотреть в окне **вывод** .

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>Добавление классов запуска

В этом разделе мы добавим еще один класс Startup. В приложение можно добавить несколько классов запуска OWIN. Например, может потребоваться создать классы запуска для разработки, тестирования и производства.

1. Создайте новый класс запуска OWIN и назовите его `ProductionStartup`.
2. Замените сгенерированный код следующим кодом:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. Нажмите клавишу Control F5, чтобы запустить приложение. Атрибут `OwinStartup` указывает, что запущен рабочий класс запуска.

    ![](owin-startup-class-detection/_static/image6.png)
4. Создайте другой класс запуска OWIN и назовите его `TestStartup`.
5. Замените сгенерированный код следующим кодом:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   Перегрузка атрибута `OwinStartup` выше указывает `TestingConfiguration` как *понятное* имя класса запуска.
6. Откройте файл *Web. config* и добавьте ключ запуска приложения OWIN, который указывает понятное имя класса Startup:

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. Нажмите клавишу Control F5, чтобы запустить приложение. Элемент параметров приложения имеет приоритет и выполняется конфигурация теста.

    ![](owin-startup-class-detection/_static/image7.png)
8. Удалите *понятное* имя из атрибута `OwinStartup` в классе `TestStartup`.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. Замените ключ запуска приложения OWIN в файле *Web. config* следующим образом:

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. Верните атрибут `OwinStartup` в каждом классе в код атрибута по умолчанию, созданный Visual Studio:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    Каждый из ключей запуска приложения OWIN, приведенных ниже, приведет к запуску рабочего класса.

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    Последний ключ запуска задает метод конфигурации запуска. Следующий ключ запуска приложения OWIN позволяет изменить имя класса конфигурации на `MyConfiguration`.

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>Использование Овинхост. exe

1. Замените файл Web. config следующей разметкой:

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   Последний ключ WINS, поэтому в данном случае `TestStartup` указан.
2. Установите Овинхост из PMC:

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. Перейдите в папку приложения (папку, содержащую файл *Web. config* ) и в командной строке введите:

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   В командном окне отобразится следующее:

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. Запустите браузер с URL-адресом `http://localhost:5000/`.

    ![](owin-startup-class-detection/_static/image8.png)

   Овинхост учитывает приведенные выше соглашения о запуске.
5. В окне командной строки нажмите клавишу ВВОД, чтобы выйти из Овинхост.
6. В классе `ProductionStartup` добавьте следующий атрибут Овинстартуп, указывающий понятное имя *продуктионконфигуратион*.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. В командной строке введите:

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   Загружается класс рабочего запуска.
    ![](owin-startup-class-detection/_static/image9.png)

   Наше приложение имеет несколько классов запуска, и в этом примере мы отложили, какой класс запуска будет загружаться до выполнения.
8. Проверьте следующие параметры запуска среды выполнения:

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
