---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: Учебник. Использование подключения устойчивость и команда перехвата с EF в приложении ASP.NET MVC
author: tdykstra
description: В этом руководстве вы узнаете, как использовать перехвата устойчивость и команду подключения. Они являются две важные функции Entity Framework 6.
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 276266f8ae9df38529d44742ebe6ac0dc8e79727
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025901"
---
# <a name="tutorial-use-connection-resiliency-and-command-interception-with-entity-framework-in-an-aspnet-mvc-app"></a>Учебник. Использование перехвата устойчивость и команду подключения с Entity Framework в приложении ASP.NET MVC

Пока приложение будет выполняться локально в IIS Express на компьютере разработчика. Чтобы реальных приложение стало доступным для других пользователей в Интернете, необходимо развернуть его на веб-поставщик услуг размещения и у вас есть развертывание базы данных на сервер базы данных.

В этом руководстве вы узнаете, как использовать перехвата устойчивость и команду подключения. Они являются две важные функции Entity Framework 6, которые особенно важны при развертывании в облачной среде: устойчивость подключений (автоматические повторы для временных ошибок) и перехват команд (catch все SQL-запросы, отправляемые базе данных для входа или изменять их).

Учебником подключения устойчивость и команда перехвата является необязательным. Если вы пропустите это руководство, будет лишь небольшие изменения, внесенные в последующих руководствах.

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Включить устойчивость подключений
> * Включить перехват команд
> * Протестируйте новую конфигурацию

## <a name="prerequisites"></a>Предварительные требования

* [Сортировка, фильтрация и разбиение на страницы](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-connection-resiliency"></a>Включить устойчивость подключений

При развертывании приложения в Windows Azure, используется для развертывания базы данных в базу данных SQL Azure Windows, облачная служба баз данных. При подключении к облачная служба баз данных, чем при веб-сервер и сервер базы данных непосредственно соединены друг с другом в одном центре обработки данных, временных ошибок подключения обычно чаще. Даже если веб-сервер cloud и облачная служба баз данных размещаются в одном центре обработки данных, существуют дополнительные сетевые подключения между ними, которые могут возникнуть проблемы, такие как подсистемы балансировки нагрузки.

Также это облачная служба обычно совместно используется другими пользователями, это означает, что отклик может зависеть от их. И доступ к базе данных может быть подвергаются регулированию. Регулирование означает, что служба базы данных создает исключения, при попытке доступа к нему дополнительные часто не допускается в вашей уровень соглашения об уровне обслуживания.

Многие или большинство проблем подключения при обращении к облачной службе являются временными, то есть они устранить самостоятельно за короткий период времени. Поэтому при попытке выполнения операции базы данных получить тип ошибки, обычно временное, можно попробовать операцию после короткого ожидания и операции может пройти успешно. Можно предоставить значительно удобней для пользователей, если обработка временных ошибок с автоматически повторить попытку, невидимую большинство из них для клиента. Функция устойчивости подключений в Entity Framework 6 автоматизирует, что процесс повторного не удалось выполнить SQL-запросов.

Функция устойчивости подключений должен быть настроен для определенной базы данных службы:

- Он должен знать, какие исключения могут быть временными. Вы хотите повторить попытку ошибки, вызванные временная потеря в сетевое подключение не ошибки, например из-за ошибок программы.
- Она должна ожидать соответствующий период времени между повторными попытками, сбой операции. Вы можете ожидать больше между повторными попытками для пакетной обработки, чем вы можете на интерактивной веб-странице, где пользователь ожидает ответа.
- Он должен повторить попытку на соответствующее число раз, прежде чем прекратить попытки. Может потребоваться повторить несколько раз в рамках пакетного процесса, как в интерактивном приложении.

Можно настроить эти параметры вручную для любой среды базы данных, поддерживаемом поставщиком Entity Framework, но уже были настроены значения по умолчанию, которые обычно доступны также в интерактивном приложении, использующем базу данных SQL Azure Windows, и Это параметры, которые вы реализуете для приложения университета Contoso.

Вам нужно выполнить, чтобы включить устойчивость подключения создать класс в сборке, производный от [DbConfiguration](https://msdn.microsoft.com/data/jj680699.aspx) и в этом классе присвоить базе данных SQL *стратегия выполнения*, в EF – еще один термин для *политика повтора*.

1. В папке DAL, добавьте файл класса с именем *SchoolConfiguration.cs*.
2. Замените код шаблона следующим кодом:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    Платформа Entity Framework автоматически выполняет код в класс, производный от `DbConfiguration`. Можно использовать `DbConfiguration` класса, чтобы выполнять задачи по настройке в коде, в противном случае это делается в *Web.config* файл. Дополнительные сведения см. в разделе [EntityFramework конфигурация на основе кода](https://msdn.microsoft.com/data/jj680699).
3. В *StudentController.cs*, добавьте `using` инструкции для `System.Data.Entity.Infrastructure`.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. Изменить все `catch` блокирует перехвата `DataException` исключения, чтобы они перехватывать `RetryLimitExceededException` исключения вместо этого. Пример:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    Вы использовали `DataException` выявления ошибок, которые могут быть временными, чтобы обеспечить понятное сообщение «повторить». Но теперь, когда вы включили политику повтора, единственные ошибки, скорее всего, будут временными будет уже были испытаны и не удалось несколько раз, и фактическое возвращаемое исключение будет вставлено в `RetryLimitExceededException` исключение.

Дополнительные сведения см. в разделе [Entity Framework Connection Resiliency / логика повторных попыток](https://msdn.microsoft.com/data/dn456835).

## <a name="enable-command-interception"></a>Включить перехват команд

Теперь, когда вы включили политику повтора, как протестировать чтобы убедиться, что он работает должным образом? Это не так просто заставить временная ошибка происходит, особенно при работе локально, и было бы особенно трудно интегрировать фактическое временных ошибок в автоматизированные модульные тест. Чтобы протестировать функция устойчивости подключений, нужен способ перехватывать запросы, которые отправляет Entity Framework для SQL Server и замените типа исключения, которое обычно временное ответ от сервера SQL.

Перехват запросов также можно использовать для реализации рекомендации для облачных приложений: [журнала задержки и успешность всех вызовов к внешним службам](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) такие как службы базы данных. Предоставляет EF6 [выделенной API ведения журнала](https://msdn.microsoft.com/data/dn469464) , можно упростить его сделать ведения журнала, но в этом разделе руководства вы узнаете, как использовать Entity Framework [механизма перехвата](https://msdn.microsoft.com/data/dn469464) напрямую, как для Ведение журнала и для имитации временных ошибок.

### <a name="create-a-logging-interface-and-class"></a>Создайте класс и интерфейс ведения журнала

Объект [рекомендация для ведения журнала](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) — это с помощью интерфейса вместо жестко запрограммированного вызовы методов System.Diagnostics.Trace или класса ведения журнала. Что упрощает изменение вашего механизма ведения позже, если вы захотите это сделать. Поэтому в этом разделе мы создадим интерфейс ведения журнала и класса для реализации его/p >

1. Создание папки в проект и назовите его *ведение журнала*.
2. В *ведение журнала* папке создайте файл класса с именем *ILogger.cs*и замените код шаблона следующим кодом:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    Этот интерфейс предоставляет три уровня трассировки, чтобы указать относительную важность журналы и один, предоставляет сведения о задержке для внешней службы вызовы, такие как запросы к базе данных. Методы ведения журнала имеют перегрузки, которые позволяют передавать исключение. Это так, что сведения об исключении, включая стек трассировки и внутренние исключения надежно регистрируется классом, который реализует интерфейс, а не полагаться на который выполняется в каждом вызове метода ведения журнала в приложении.

    Методы TraceApi позволяют отслеживать задержку каждого вызова определенной внешней службы, такие как базы данных SQL.
3. В *ведение журнала* папке создайте файл класса с именем *Logger.cs*и замените код шаблона следующим кодом:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    Реализация использует System.Diagnostics для трассировки. Это встроенная функция .NET, что позволяет легко создать и использовать данные трассировки. Существует много «прослушиватели» можно использовать с трассировкой System.Diagnostics записывать журналы к файлам, к примеру, или для записи их в хранилище BLOB-объектов Azure. Некоторые из вариантов, а также ссылки на другие ресурсы, Дополнительные сведения см. в [Устранение неполадок веб-сайтов Azure в Visual Studio](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio). Этот учебник позволяет только просмотреть журналы в Visual Studio **вывода** окна.

    В рабочем приложении может потребоваться учитывать пакеты трассировки, отличный от System.Diagnostics и интерфейс ILogger позволяет относительно легко переключиться на механизм разных трассировки, если вы решили сделать это.

### <a name="create-interceptor-classes"></a>Создайте перехватчик классы

Теперь необходимо создать классы, которые Entity Framework будет вызывать каждый раз, когда оно для отправки запроса к базе данных для имитации временных ошибок и сделать ведения журнала. Эти классы перехватчик должен быть производным от `DbCommandInterceptor` класса. В них вы напишете переопределения методов, которые вызываются автоматически в том случае, когда запрос будет выполняться. В этих методах можно изучать или запрос, который отправляется в базу данных к журналу, а также можно изменить запрос перед отправкой в базу данных или возвращать результат Entity Framework самостоятельно без даже передача запроса к базе данных.

1. Чтобы создать класс перехватчик, которая будет записывать каждый запрос SQL, который отправляется в базу данных, создайте файл класса с именем *SchoolInterceptorLogging.cs* в *DAL* папку и замените код шаблона Следующий код:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    Для успешно выполненных запросов или команд этот код записывает в журнал сведения с сведения о задержке. Для исключений он создает журнал ошибок.
2. Для создания класса-перехватчика, вызывающая фиктивный временных ошибок при вводе «Throw» в **поиска** поле, создайте файл класса с именем *SchoolInterceptorTransientErrors.cs* в *DAL* папку и замените код шаблона следующим кодом:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    Этот код только переопределения `ReaderExecuting` метод, который вызывается для запросов, которые могут возвращать несколько строк данных. Если вы хотите проверить устойчивость подключения для других типов запросов, можно также переопределить `NonQueryExecuting` и `ScalarExecuting` методы, как ведение журнала перехватчик.

    При запуске страницы учащихся и введите «Throw» в строке поиска, этот код создает фиктивный исключение базы данных SQL для номер ошибки 20, типом, известным обычно временной. Другие коды ошибок, момент опознаны как временные являются 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501 и 40613, но они могут быть изменены в новые версии базы данных SQL.

    Код возвращает исключение в Entity Framework, вместо выполнения запроса и передачи результатов запроса назад. Временное исключение возвращается в четыре раза, а затем код возвращается к обычной процедуры передачи запроса к базе данных.

    Так как все, что в системе, вы сможете см. в разделе Entity Framework пытается выполнить запрос предшествовало в четыре раза, что в приложении отличается только что занимает больше времени для визуализации страницы с результатами запроса.

    Количество раз, когда Entity Framework будет повторять попытку настраивается; код определяет четыре раза, потому что это значение по умолчанию для политики выполнения базы данных SQL. Если изменить политику выполнения, необходимо было также изменение здесь расположен код, указывает, сколько раз создаются временные ошибки. Можно также изменить код, чтобы создать дополнительные исключения, чтобы платформа Entity Framework вызывает исключение `RetryLimitExceededException` исключение.

    Значение, указанное в поле поиска будет находиться в `command.Parameters[0]` и `command.Parameters[1]` (один используется имя и фамилия). Если найдено значение «% Throw %», «Throw» заменяется в эти параметры «», чтобы некоторые студенты будут найдены и возвращается.

    Это просто удобный способ проверить устойчивость подключений, в зависимости от изменяющихся некоторые входные данные для пользовательского интерфейса приложения. Можно также написать код для создания временных ошибок для всех запросов или обновлений, как описано далее в комментарии о *DbInterception.Add* метод.
3. В *Global.asax*, добавьте следующий `using` инструкции:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. Добавьте выделенные строки, чтобы `Application_Start` метод:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    Эти строки кода являются, что вызывает перехватчик кода для запуска в том случае, когда Entity Framework отправляет запросы к базе данных. Обратите внимание, что так как вы создали отдельные перехватчик классы для имитации временных ошибок и ведение журнала, вы можете независимо друг от друга, включить или отключить их.

    Можно добавить с помощью перехватчики `DbInterception.Add` метод в любом месте кода; он не должен быть в `Application_Start` метод. Другой вариант — поместить этот код в класс DbConfiguration, который был создан ранее, чтобы настроить политику выполнения.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    Везде, где поместить этот код, нужно избегать выполнения `DbInterception.Add` для же перехватчик более чем один раз, или вы получите дополнительные перехватчик экземпляров. Например если дважды добавить перехватчик ведения журнала, вы увидите два журнала для каждого запроса SQL.

    Перехватчики выполняются в порядке регистрации (порядок, в котором `DbInterception.Add` вызывается метод). Порядок может имеет значения в зависимости от выполняемых задач в перехватчик. Например, перехватчик может изменить команду SQL, получаемый в `CommandText` свойство. Если это приводит к изменению команду SQL, далее перехватчик получите измененные команду SQL, не исходную команду SQL.

    Вы написали код имитации временной ошибки способом, который позволяет вызывать временные ошибки, введя другое значение в пользовательском Интерфейсе. Кроме того можно написать код перехватчик всегда создать последовательность временных исключений без проверки на наличие значения определенного параметра. Затем вы сможете добавить перехватчик только в том случае, если вы хотите создавать временные ошибки. Если в этом случае не добавляйте перехватчик до после завершения инициализации базы данных. Другими словами выполните операции по крайней мере одна база данных, например запрос на одном из своего набора сущностей, перед началом создания временных ошибок. Платформа Entity Framework выполняет несколько запросов во время инициализации базы данных, и они не выполняются в транзакции, в случае ошибки во время инициализации может возникнуть контекст которого необходимо получить в несогласованное состояние.

## <a name="test-the-new-configuration"></a>Протестируйте новую конфигурацию

1. Нажмите клавишу **F5** запустите приложение в режиме отладки, и нажмите кнопку **учащихся** вкладки.
2. Посмотрите на Visual Studio **вывода** окно, чтобы просмотреть выходные данные трассировки. Может потребоваться прокрутить вверх после некоторых ошибок JavaScript, чтобы получить журналы, сохраняемые в средство ведения журналов.

    Обратите внимание на то, что вы видите фактические SQL-запросы, отправляемые в базу данных. Вы увидите некоторые начальные запросы и команды, которые Entity Framework выполняет обновление, чтобы приступить к работе, проверка версии базы данных и таблицы журнала миграции (вы узнаете о миграции в следующем учебном курсе). Появится запрос для разбиения на страницы, чтобы узнать, сколько учащихся, и наконец видеть запрос, который получает данные об учащихся.

    ![Ведение журнала для обычный запрос](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. В **учащихся** странице введите «Throw» в строке поиска и нажмите кнопку **поиска**.

    ![Создать строку поиска](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    Вы заметите, что браузер кажется зависает на несколько секунд, пока Entity Framework повторением запроса несколько раз. Первый Повтор происходит очень быстро, затем ожидать увеличения перед каждой следующей попытки. Процесс больше ожидания перед каждым повтором называется *экспоненциального откладывания*.

    При отображении страницы отображение учащиеся имеют «значение» в именах, посмотрите в окно вывода, и вы увидите, что тот же запрос количество предпринятых попыток пяти, первые четыре раза возвращением временных исключений. Для каждой временной ошибки вы увидите журнала, создаваемого при создании временной ошибке в `SchoolInterceptorTransientErrors` класс («возвращение временная ошибка команды...») и вы увидите журнала, записанных при `SchoolInterceptorLogging` возвращает исключение.

    ![Выходные данные ведения журнала с повторными попытками](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    Так как вы ввели строку поиска, параметризован запрос, который возвращает данные об учащихся:

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    Значения параметров не выполняется вход, но это можно сделать. Если вы хотите просмотреть значения параметра, можно написать код ведения журнала, чтобы получить значения параметров из `Parameters` свойство `DbCommand` объект, который вы получаете в методы перехватчика.

    Обратите внимание на то, что нельзя повторите этот тест, если вы остановите приложение и перезапустите его. Если вы хотите иметь возможность тестировать устойчивость подключения несколько раз в рамках одного запуска приложения, можно написать код, чтобы сбросить счетчик ошибок в `SchoolInterceptorTransientErrors`.
4. Чтобы увидеть разницу стратегии выполнения (политика повтора) делает, комментарий `SetExecutionStrategy` строку в *SchoolConfiguration.cs*, снова запустите на страницу учащихся в режиме отладки и повторить поиск «Throw».

    Это время отладчик останавливается на первой порожденное исключение немедленно в том случае, когда предпринимается попытка выполнения запроса в первый раз.

    ![Фиктивный исключение](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. Раскомментируйте *SetExecutionStrategy* строку в *SchoolConfiguration.cs*.

## <a name="get-the-code"></a>Получение кода

[Скачать завершенный проект](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Дополнительные ресурсы

Ссылки на другие ресурсы Entity Framework можно найти в [доступ к данным ASP.NET — рекомендуемые ресурсы](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Следующие шаги

В этом учебнике рассмотрены следующие задачи.

> [!div class="checklist"]
> * Устойчивость подключения включено
> * Перехват поддержкой команд
> * Тестирование новой конфигурации

Перейдите к следующей статьи вы узнаете о Code First migrations и развертывание Azure.
> [!div class="nextstepaction"]
> [Code First migrations и развертывание Azure](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)