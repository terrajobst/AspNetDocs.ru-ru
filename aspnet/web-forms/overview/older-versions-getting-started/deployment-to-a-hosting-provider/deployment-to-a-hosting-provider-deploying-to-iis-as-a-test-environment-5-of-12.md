---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: 'Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание в IIS в качестве тестовой среды — 5 из 12 | Документация Майкрософт'
author: tdykstra
description: В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5d85232ff2cb229d771d517db7173721c9e277bf
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633514"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание в IIS в качестве тестовой среды — 5 из 12

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web. При установке обновления веб-публикации можно также использовать Visual Studio 2010. Введение в серию см. [в первом учебнике серии](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Руководство, в котором показаны функции развертывания, появившиеся после выпуска версии-КАНДИДАТа Visual Studio 2012, демонстрирует развертывание SQL Server выпусков, отличных от SQL Server Compact, и демонстрация развертывания в веб-приложениях службы приложений Azure см. в разделе [ASP.NET Web Deploying using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Обзор

В этом руководстве показано, как развернуть веб-приложение ASP.NET в службах IIS на локальном компьютере.

При разработке приложения обычно выполняется тестирование с его запуском в Visual Studio. По умолчанию это означает, что вы используете Visual Studio Development Server (также называется Cassini). Visual Studio Development Server упрощает тестирование во время разработки в Visual Studio, но не работает точно так же, как IIS. В результате приложение может правильно работать при тестировании в Visual Studio, но при развертывании в службах IIS в среде размещения произойдет сбой.

Вы можете более надежно протестировать приложение следующими способами:

1. Используйте IIS Express или полные службы IIS вместо Visual Studio Development Server при тестировании в Visual Studio во время разработки. Как правило, этот метод имитирует более точное моделирование работы сайта в службах IIS. Однако этот метод не тестирует процесс развертывания или не проверяет, что результат процесса развертывания будет выполняться правильно.
2. Разверните приложение в службах IIS на компьютере разработчика, используя тот же процесс, который будет использоваться позже для развертывания в рабочей среде. Этот метод проверяет процесс развертывания в дополнение к проверке того, что приложение будет правильно работать в службах IIS.
3. Разверните приложение в тестовой среде, как можно ближе к рабочей среде. Так как Рабочая среда для этих учебников является сторонним поставщиком услуг размещения, идеальная тестовая среда будет второй учетной записью с поставщиком услуг размещения. Эту вторую учетную запись следует использовать только для тестирования, но она будет настроена так же, как и Рабочая учетная запись.

В этом руководстве описаны шаги для варианта 2. Рекомендации для варианта 3 приведены в конце руководства по [развертыванию в рабочей среде](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) . в конце этого руководства имеются ссылки на ресурсы для варианта 1.

Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="configuring-the-application-to-run-in-medium-trust"></a>Настройка приложения для работы в среднем доверии

Перед установкой IIS и развертыванием на нем необходимо изменить параметр файла Web. config, чтобы сделать сайт более похожим на типичную общую среду размещения.

Поставщики услуг размещения обычно запускают веб-сайт со *средним уровнем доверия*, что означает, что это не разрешено. Например, код приложения не может получить доступ к реестру Windows и не может читать или записывать файлы, находящиеся за пределами иерархии папок приложения. По умолчанию приложение работает на локальном компьютере с *высоким уровнем доверия* , что означает, что приложение может выполнять те действия, которые могут завершиться сбоем при развертывании в рабочей среде. Таким образом, чтобы убедиться в том, что тестовая среда более точно отражает рабочую среду, вы настроите приложение для работы в среднем уровне доверия.

В файле Web. config приложения добавьте элемент **Trust** в элемент **System. Web** , как показано в этом примере.

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

Теперь приложение будет работать в службах IIS со средним уровнем доверия даже на локальном компьютере. Этот параметр позволяет перехватывать как можно раньше любые попытки, выполняемые кодом приложения, что приведет к сбою в рабочей среде.

> [!NOTE]
> Если вы используете Entity Framework Code First Migrations, убедитесь, что установлена версия 5,0 или более поздняя. В Entity Framework версии 4,3 для обновления схемы базы данных миграции требуется полное доверие.

## <a name="installing-iis-and-web-deploy"></a>Установка служб IIS и веб-развертывание

Для развертывания служб IIS на компьютере разработчика необходимо установить службы IIS и веб-развертывание. Они не включены в конфигурацию Windows 7 по умолчанию. Если вы уже установили IIS и веб-развертывание, перейдите к следующему разделу.

Использование [установщика веб-платформы](https://www.microsoft.com/web/downloads/platform.aspx) является предпочтительным способом установки служб iis и веб-развертывание, поскольку установщик веб-платформы устанавливает рекомендуемую конфигурацию для IIS и автоматически устанавливает необходимые компоненты для iis и веб-развертывание при необходимости.

Чтобы запустить установщик веб-платформы для установки служб IIS и веб-развертывание, используйте следующую ссылку. Если службы IIS уже установлены, веб-развертывание или любой из необходимых компонентов, установщик веб-платформы устанавливает только то, что отсутствует.

- [Установка служб IIS и веб-развертывание с помощью установщика веб](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>Задание для пула приложений по умолчанию значения .NET 4

После установки служб IIS запустите **Диспетчер IIS** , чтобы убедиться, что .NET Framework версии 4 назначено пулу приложений по умолчанию.

В меню **Пуск** Windows выберите пункт **выполнить**, введите inetmgr и нажмите кнопку **ОК**. (Если команда **выполнить** отсутствует в меню " **Пуск** ", можно нажать клавишу Windows и R, чтобы открыть ее. Или щелкните правой кнопкой мыши панель задач, выберите пункт **Свойства**, откройте вкладку **меню Пуск** , щелкните **Настройка**и выберите **выполнить команду**.)

В области **подключения** разверните узел сервера и выберите **Пулы приложений**. Если в области **Пулы приложений** **DefaultAppPool** назначена платформа .NET Framework версии 4, как показано на следующем рисунке, перейдите к следующему разделу.

[![Inetmgr_showing_4.0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

Если вы видите только два пула приложений и оба имеют значение .NET Framework 2,0, необходимо установить ASP.NET 4 в службах IIS:

- Откройте окно командной строки, щелкнув правой кнопкой мыши пункт **Командная строка** в меню **Пуск** Windows и выбрав команду **Запуск от имени администратора**. Затем запустите [aspnet\_regiis. exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) для установки ASP.NET 4 в IIS с помощью следующих команд. (В 64-разрядных системах замените "Framework" на "Framework64".)

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![aspnet_regiis_installing_ASP. NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    Эта команда создает новые пулы приложений для .NET Framework 4, но пул приложений по умолчанию по-прежнему будет иметь значение 2,0. Вы разворачиваете приложение, предназначенное для .NET 4, для этого пула приложений, поэтому необходимо изменить пул приложений на .NET 4.

Если вы закрыли **Диспетчер IIS**, запустите его снова, разверните узел сервера и щелкните **Пулы приложений** , чтобы снова отобразить панель **Пулы приложений** .

В области **Пулы приложений** щелкните **DefaultAppPool**, а затем на панели **действия** щелкните **Основные параметры**.

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

В диалоговом окне **Изменение пула приложений** измените значение **.NET Framework версия** на **.NET Framework v 4.0.30319** и нажмите кнопку **ОК**.

[![Selecting_. NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

Теперь все готово для публикации в службах IIS.

## <a name="publishing-to-iis"></a>Публикация в службах IIS

Существует несколько способов развертывания с помощью Visual Studio 2010 и веб-развертывание.

- Используйте команду "опубликовать" одним щелчком Visual Studio.
- Создайте *пакет развертывания* и установите его с помощью пользовательского интерфейса диспетчера IIS. Пакет развертывания состоит из *ZIP* -файла, содержащего все файлы и метаданные, необходимые для установки сайта в службах IIS.
- Создайте пакет развертывания и установите его с помощью командной строки.

Процесс, который вы выполнили в предыдущих руководствах, чтобы настроить Visual Studio для автоматизации задач развертывания, применяется ко всем этим трем методам. В этих учебниках используется первый из этих методов. Дополнительные сведения об использовании пакетов развертывания см. в разделе [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx).

Перед публикацией убедитесь, что вы используете Visual Studio в режиме администратора. (В меню **Пуск** Windows 7 щелкните правой кнопкой мыши значок используемой версии Visual Studio и выберите **Запуск от имени администратора**.) Режим администратора необходим для публикации только при публикации в службах IIS на локальном компьютере.

В **Обозреватель решений**щелкните правой кнопкой мыши проект ContosoUniversity (не проект CONTOSOUNIVERSITY. DAL) и выберите **опубликовать**.

Откроется мастер **публикации веб-сайта** .

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

В раскрывающемся списке выберите **&lt;New...&gt;** .

В диалоговом окне **новый профиль** введите "Test" и нажмите кнопку **ОК**.

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

Это имя совпадает с средним узлом созданного ранее файла преобразования Web. Test. config. Эта корреспонденция является причиной применения преобразований Web. Test. config при публикации с помощью этого профиля.

Мастер автоматически перейдет на вкладку **Connection (подключение** ).

В поле **URL-адрес службы** введите *localhost*.

В поле **сайт/приложение** введите *Default Web site/ContosoUniversity*.

В поле **URL-адрес назначения** введите `http://localhost/ContosoUniversity`.

Параметр **URL-адреса назначения** не является обязательным. Когда Visual Studio завершит развертывание приложения, автоматически откроется браузер по умолчанию с этим URL-адресом. Если вы не хотите, чтобы браузер открывался автоматически после развертывания, оставьте это поле пустым.

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

Щелкните **проверить подключение** , чтобы убедиться, что параметры заданы правильно, и вы можете подключиться к службам IIS на локальном компьютере.

Зеленая галочка проверяет, успешно ли установлено соединение.

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

Нажмите кнопку **Далее** , чтобы перейти на вкладку **Параметры** .

В раскрывающемся списке **Конфигурация** указывается развертываемая конфигурация сборки. Значение по умолчанию — Release, что нужно сделать.

Оставьте флажок **удалить дополнительные файлы в месте назначения** снятым. Так как это первое развертывание, в папке назначения еще не будет файлов.

В разделе **базы данных** введите следующее значение в поле Строка подключения для **SchoolContext**:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

Процесс развертывания поместит эту строку подключения в развернутый файл Web. config, поскольку выбран параметр **использовать эту строку подключения во время выполнения** .

Кроме того, в разделе **SchoolContext**выберите **применить Code First migrations**. Этот параметр приводит к тому, что процесс развертывания настраивает развернутый файл Web. config для указания инициализатора `MigrateDatabaseToLatestVersion`. Этот инициализатор автоматически обновляет базу данных до последней версии, когда приложение обращается к базе данных в первый раз после развертывания.

В поле Строка подключения для **DefaultConnection**введите следующее значение:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

Не снимайте флажок **обновлять базу данных** . База данных членства будет развернута путем копирования SDF-файла в приложение\_данных, и вы не хотите, чтобы процесс развертывания ни в чем еще больше не затронула эту базу данных.

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

Нажмите кнопку **Далее** , чтобы перейти на вкладку **Предварительный просмотр** .

На вкладке **Предварительный просмотр** нажмите кнопку **начать предварительный просмотр** , чтобы просмотреть список файлов, которые будут скопированы.

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

Нажмите кнопку **Опубликовать**.

Если Visual Studio не находится в режиме администратора, может появиться сообщение об ошибке, указывающее на ошибку разрешений. В этом случае закройте Visual Studio, откройте его в режиме администратора и повторите попытку публикации.

Если Visual Studio находится в режиме администратора, окно **вывода** сообщает об успешной сборке и публикации.

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

Браузер автоматически откроется на домашней странице университета Contoso, запущенной в службах IIS на локальном компьютере.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>Тестирование в тестовой среде

Обратите внимание, что индикатор среды отображает "(тест)" вместо "(dev)", что показывает, что преобразование *Web. config* для индикатора среды прошло успешно.

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

Запустите страницу **учащихся** , чтобы убедиться, что развернутая база данных не содержит учащихся. При выборе этой страницы Загрузка может занять несколько минут, поскольку Code First создает базу данных, а затем запускает метод `Seed`. (Это не было сделано, когда вы находились на домашней странице, так как приложение еще не пытается получить доступ к базе данных.)

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

Запустите страницу **инструкторы** , чтобы убедиться, что Code First заполнена базой данных с помощью инструкторов:

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

Выберите **Добавить учащихся** в меню **учащихся** , добавьте учащийся, а затем просмотрите новый учащийся на странице **учащихся** , чтобы убедиться, что вы можете успешно выполнить запись в базу данных:

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

В меню **курсы** выберите **Обновить кредиты**. На странице " **Обновление кредитов** " требуются разрешения администратора, поэтому отображается страница **входа** . Введите учетные данные администратора, созданные ранее ("admin" и "PAS $ w0rd"). Отобразится страница **Обновление кредитов** , которая подтверждает, что учетная запись администратора, созданная в предыдущем руководстве, правильно развернута в тестовой среде.

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

Убедитесь, что папка *ELMAH* существует только в файле заполнителя.

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>Просмотр автоматических изменений Web. config для Code First Migrations

Откройте файл *Web. config* в развернутом приложении на сайте *к:\инетпуб\ввврут\контосауниверсити* , и вы увидите, где в процессе развертывания настроен Code First migrations для автоматического обновления базы данных до последней версии.

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

В процессе развертывания также создается новая строка подключения для Code First Migrations для использования исключительно для обновления схемы базы данных.

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

Эта дополнительная строка подключения позволяет указать одну учетную запись пользователя для обновлений схемы базы данных и другую учетную запись пользователя для доступа к данным приложения. Например, можно назначить роль\_владельца базы данных Code First Migrations, а\_DB и Database\_DB — приложению. Это распространенный шаблон глубокой защиты, который предотвращает изменение схемы базы данных потенциально вредоносным кодом в приложении. (Например, это может произойти при успешной атаке путем внедрения кода SQL.) Этот шаблон не используется в этих учебниках. Он не применяется к SQL Server Compact и не применяется при переходе на SQL Server в последующем учебнике этой серии. Сайт Цитаниум предлагает только одну учетную запись пользователя для доступа к базе данных SQL Server, созданной на Цитаниум. Если вы можете реализовать этот шаблон в своем сценарии, это можно сделать, выполнив следующие действия.

1. На вкладке **Параметры** мастера **публикации веб-сайта** введите строку подключения, которая указывает пользователя с полными разрешениями на обновление схемы базы данных, и снимите флажок **использовать эту строку подключения во время выполнения** . В развернутом файле Web. config он преобразуется в строку подключения `DatabasePublish`.
2. Создайте преобразование файла Web. config для строки подключения, которую приложение должно использовать во время выполнения.

Теперь вы развернули приложение в службах IIS на компьютере разработчика и протестировали его там. Это подтверждает, что процесс развертывания скопировал содержимое приложения в нужное расположение (за исключением файлов, которые вы не хотите развертывать), а также веб-развертывание правильно настроить IIS во время развертывания. В следующем руководстве вы выполните еще один тест, который находит еще не выполненную задачу развертывания: Задание разрешений для папки в папке *ELMAH* .

## <a name="more-information"></a>Дополнительные сведения

Сведения о запуске IIS или IIS Express в Visual Studio см. в следующих ресурсах:

- [IIS Express обзор](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) сайта IIS.NET.
- [Введение IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) в блог Скотта Гатри (.
- [Как указать веб-сервер для веб-проектов в Visual Studio](https://msdn.microsoft.com/library/ms178108.aspx).
- [Основные различия между IIS и ASP.NET Development Server](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) на сайте ASP.NET.
- [Протестируйте приложение ASP.NET MVC или Web Forms в IIS 7 за 30 секунд](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx) в блоге Рик Андерсон (. Эта запись содержит примеры того, почему тестирование с Visual Studio Development Server (Cassini) не так надежно, как тестирование в IIS Express, и почему тестирование в IIS Express не так надежно, как тестирование в службах IIS.

Сведения о проблемах, которые могут возникнуть при работе приложения со средним уровнем доверия, см. в разделе [размещение ASP.NET приложений на среднем уровне доверия](http://www.4guysfromrolla.com/articles/100307-1.aspx) в 4 ролла сайта.

> [!div class="step-by-step"]
> [Назад](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [Вперед](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
