---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 'Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание в рабочей среде — 7 из 12 | Документация Майкрософт'
author: tdykstra
description: В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: db838633accdedd7c0693b126a007e254ca681e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458172"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание в рабочей среде — 7 из 12

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web. При установке обновления веб-публикации можно также использовать Visual Studio 2010. Введение в серию см. [в первом учебнике серии](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Руководство, в котором показаны функции развертывания, появившиеся после выпуска версии-КАНДИДАТа Visual Studio 2012, демонстрирует развертывание SQL Server выпусков, отличных от SQL Server Compact, и демонстрация развертывания в веб-приложениях службы приложений Azure см. в разделе [ASP.NET Web Deploying using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Обзор

В этом руководстве вы настроите учетную запись с поставщиком услуг размещения и развернете веб-приложение ASP.NET в рабочей среде с помощью функции публикации одним щелчком в Visual Studio.

Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="selecting-a-hosting-provider"></a>Выбор поставщика услуг размещения

Для приложения университета Contoso и этой серии руководств требуется поставщик, поддерживающий ASP.NET 4 и веб-развертывание. Была выбрана конкретная компания по размещению, чтобы в руководствах были показаны все возможности развертывания на веб-сайте в реальном времени. Каждая компания размещения предоставляет различные функции, и процесс развертывания на серверах несколько отличается. Однако процесс, описанный в этом руководстве, является типичным для всего процесса. Поставщик услуг размещения, используемый для этого учебника, Cytanium.com, является одним из множества доступных, и его использование в этом руководстве не является рекомендацией или рекомендациями.

Когда вы будете готовы выбрать собственного поставщика услуг размещения, вы можете сравнить функции и цены в [коллекции поставщиков](https://www.microsoft.com/web/hosting) на сайте Microsoft.com/Web.

## <a name="creating-an-account"></a>Создание учетной записи

Создайте учетную запись в выбранном поставщике. Если поддержка полной SQL Server базы данных является дополнительным, вам не нужно выбирать ее для работы с этим руководством, но это потребуется для [перехода на SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) учебнике далее в этой серии.

Для этих учебников не нужно регистрировать новое доменное имя. Проверить успешность развертывания можно с помощью временного URL-адреса, назначенного сайту поставщиком.

После создания учетной записи вы обычно получаете приветственное сообщение электронной почты, содержащее всю необходимую информацию для развертывания и управления сайтом. Сведения, которые отправляет поставщик услуг размещения, будут аналогичны приведенным здесь. Приветственное сообщение Цитаниум, отправляемое новым владельцам учетных записей, содержит следующие сведения:

- URL-адрес сайта панели управления поставщика, на котором можно управлять параметрами сайта. Указанные вами идентификатор и пароль включены в эту часть приветственного сообщения электронной почты для справки. (Оба были изменены на демонстрационное значение для этой иллюстрации.)

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- Версия .NET Framework по умолчанию и информация о том, как ее изменить. Многие сайты размещения по умолчанию имеют значение 2,0, которое работает с ASP.NET приложениями, предназначенными для .NET Framework 2,0, 3,0 или 3,5. Однако университет Contoso — это приложение .NET Framework 4, поэтому необходимо изменить этот параметр. (Для приложения ASP.NET 4,5 следует использовать параметр .NET 4,0.)

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- Временный URL-адрес, который вы можете использовать для доступа к вашему сайту. При создании этой учетной записи в качестве существующего доменного имени была указана «contosouniversity.com». Поэтому временный URL-адрес `http://contosouniversity.com.vserver01.cytanium.com`.

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- Сведения о том, как настроить базы данных и строки подключения, необходимые для доступа к ним:

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- Сведения о средствах и параметрах для развертывания сайта. (В сообщении электронной почты от Цитаниум также упоминается WebMatrix, который здесь опускается.)

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>Задание версии .NET Framework

Приветственное сообщение Цитаниум содержит ссылку на инструкции по изменению версии .NET Framework. Эти инструкции объясняют, что это можно сделать с помощью панели управления Цитаниум. Другие поставщики имеют узлы панели управления, которые выглядят иначе, или они могут попытаться сделать это другим способом.

Перейдите на страницу URL-адрес панели управления. После входа с использованием имени пользователя и пароля отобразится панель управления.

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

В поле **пространства размещения** наведите указатель мыши на значок веб-сайта и выберите в меню пункт **веб-сайты** .

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

В поле **веб-сайты** щелкните **contosouniversity.com** (имя сайта, которое использовалось при создании учетной записи).

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

В диалоговом окне **Свойства веб-сайта** перейдите на вкладку **расширения** .

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

Измените ASP.NET с **интегрированного конвейера 2,0** на **4,0 (интегрированный конвейер)** и нажмите кнопку **Обновить**.

## <a name="publishing-to-the-hosting-provider"></a>Публикация в поставщике услуг размещения

Приветственное сообщение от поставщика услуг размещения включает все параметры, необходимые для публикации проекта. Эти сведения можно ввести вручную в профиль публикации. Но вы будете использовать простой и менее подверженный ошибкам метод настройки развертывания для поставщика: вы скачиваете *publishsettings* -файл и импортируете его в профиль публикации.

В браузере перейдите на панель управления Цитаниум и выберите **веб** - **сайты.**

![Панель управления "Выбор веб-сайтов"](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

Выберите веб-сайт **contosouniversity.com** .

![Панель управления выбор contosouniversity.com](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

Перейдите на вкладку **веб-публикация** .

![Вкладка веб-публикация панели управления](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

Создайте учетные данные, используемые для веб-публикации, введя имя пользователя и пароль. Вы можете ввести те же учетные данные, которые используются для входа в систему на панели управления. Затем щелкните **Включить**.

![Панель управления "Создание учетных данных публикации"](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

Щелкните **скачать профиль публикации для этого веб-сайта**.

![Загрузить профиль публикации на панели управления](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

При появлении запроса на открытие или сохранение файла сохраните его.

![Сохранить файл профиля публикации](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

В **Обозреватель решений** в Visual Studio щелкните правой кнопкой мыши проект ContosoUniversity и выберите **Publish (опубликовать**). Диалоговое окно **Публикация веб-сайта** открывается на вкладке **Предварительный просмотр** с выбранным профилем **тестирования** , поскольку это последний использованный профиль.

Перейдите на вкладку **профиль** и нажмите кнопку **Импорт**.

![Кнопка импорта мастера публикации веб-сайта](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

В диалоговом окне **Импорт параметров публикации** выберите скачанный файл *publishsettings* и нажмите кнопку **Открыть**. Мастер переходит на вкладку Подключение со всеми заполненными полями.

![Вкладка подключения мастера публикации веб-сайта](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

Файл. publishsettings помещает в поле URL-адреса запланированный постоянный URL-адрес сайта, но если вы еще не приобрели этот домен, замените значение временным URL-адресом. В этом примере URL-адрес  *[http://contosouniversity.com.vserver01.cytanium.com](http://contosouniversity.com.vserver01.cytanium.com).* Единственное назначение этого поля — указать URL-адрес, который браузер будет открывать автоматически после успешного развертывания. Если оставить его пустым, единственное следствие заключается в том, что браузер не запустится автоматически после развертывания.

Щелкните **проверить подключение** , чтобы убедиться, что параметры заданы правильно, и вы можете подключиться к серверу. Как было показано ранее, зеленая галочка означает, что соединение прошло успешно.

При нажатии кнопки Проверить подключение может отобразиться диалоговое окно **Ошибка сертификата** . В этом случае убедитесь, что имя сервера отличается от предполагаемого. Если это так, выберите **сохранить этот сертификат для будущих сеансов Visual Studio** и нажмите кнопку **принять**. (Эта ошибка означает, что поставщик услуг размещения решил избежать расходов на приобретение сертификата SSL для URL-адреса, на который выполняется развертывание. Если вы предпочитаете установить безопасное подключение с помощью действительного сертификата, обратитесь к поставщику услуг размещения.)

![Ошибка сертификата](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

Щелкните **Далее**.

В разделе **базы данных** на вкладке **Параметры** введите те же значения, которые были введены для профиля тестовой публикации. Нужные строки подключения можно найти в раскрывающихся списках.

- В поле Строка подключения для **SchoolContext** выберите `Data Source=|DataDirectory|School-Prod.sdf`
- В разделе **SchoolContext**выберите **применить Code First migrations**.
- В поле Строка подключения для **DefaultConnection**выберите `Data Source=|DataDirectory|aspnet-Prod.sdf`
- В разделе **DefaultConnection**оставьте поле **обновить базу данных** не выбрано.

![Вкладка параметров мастера публикации веб-сайта](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

Щелкните **Далее**.

На вкладке **Предварительный просмотр** нажмите кнопку **начать предварительный просмотр** , чтобы просмотреть список файлов, которые будут скопированы. Вы увидите тот же список, который вы видели ранее при развертывании служб IIS на локальном компьютере.

Перед публикацией измените имя профиля таким образом, чтобы файл преобразования Web. Production. config будет применен. Перейдите на вкладку **профиль** и щелкните **Управление профилями**.

![Мастер публикации веб-сайта Управление профилями](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

В диалоговом окне **изменение профилей веб-публикации** выберите профиль рабочей среды, нажмите кнопку **Переименовать**и измените имя профиля на Рабочая. Затем нажмите кнопку **Закрыть**.

![Диалоговое окно «изменение профилей веб-публикации»](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

Щелкните **Опубликовать**.

Приложение публикуется в поставщике услуг размещения. Результат отображается в окне **вывод** .

![Окно вывода после развертывания](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

Браузер автоматически откроется на URL-адресе, введенном в поле **URL-адрес назначения** на вкладке **Подключение** мастера **публикации веб-сайта** . Вы увидите ту же домашнюю страницу, что и при запуске сайта в Visual Studio, за исключением того, что в заголовке окна отсутствует индикатор среды "(тест)" или "(dev)". Это означает, что преобразование " *Web. config* " индикатора среды работало правильно.

> [!NOTE]
> Если в заголовке по-прежнему отображается "(тест)", удалите папку *obj* из проекта ContosoUniversity и выполните повторное развертывание. В предварительных версиях программного обеспечения ранее примененный файл преобразования (Web. Test. config) может быть применен повторно, несмотря на то, что используется рабочий профиль.

[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

Перед запуском страницы, которая вызывает доступ к базе данных, убедитесь, что ELMAH сможет регистрировать все произошедшие ошибки.

## <a name="setting-folder-permissions-for-elmah"></a>Настройка разрешений папки для ELMAH

Как вы помните из предыдущего руководства в этой серии, необходимо убедиться, что приложение имеет разрешения на запись для папки в приложении, в которой ELMAH хранит файлы журнала ошибок. При развертывании служб IIS локально на компьютере эти разрешения устанавливаются вручную. В этом разделе вы узнаете, как задать разрешения на Цитаниум. (Некоторые поставщики услуг размещения могут не позволить это сделать. они могут предложить одну или несколько предопределенных папок с разрешениями на запись. В этом случае потребуется изменить приложение для использования указанных папок.)

Разрешения папки можно задать на панели управления Цитаниум. Перейдите на страницу URL-адрес панели управления и выберите **Диспетчер файлов**.

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

В поле **Диспетчер файлов** выберите **contosouniversity.com** и **wwwroot** , чтобы увидеть корневую папку приложения. Щелкните значок замка рядом с **ELMAH**.

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

В окне **разрешения папки**/**файлов** установите флажки **Чтение** и **запись** для **contosouniversity.com** и нажмите кнопку **задать разрешения**.

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

Убедитесь, что ELMAH имеет доступ на запись к папке *ELMAH* , вызывая ошибку, а затем отображая отчет об ошибках ELMAH. Запросите недопустимый URL-адрес, например *студентскскскс. aspx*. Как и раньше, отобразится страница *женерицеррорпаже. aspx* . Щелкните ссылку **выход** и запустите *ELMAH. axd*. Сначала вы получаете страницу **входа** , которая подтверждает, что преобразование *Web. config* успешно добавило авторизацию ELMAH. После входа в систему появится отчет, показывающий ошибку, которую вы только что вызывали.

[![ELMAH. axd_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>Тестирование в рабочей среде

Запустите страницу **учащихся** . Приложение пытается получить доступ к базе данных School в первый раз, что активирует Code First Migrations создания базы данных. Когда страница отображается после задержки, она показывает, что учащихся нет.

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

Запустите страницу **инструкторы** , чтобы убедиться, что начальные данные успешно вставили данные преподавателя в базу данных.

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

Как и в тестовой среде, необходимо убедиться, что обновления базы данных работают в рабочей среде, но обычно не требуется вводить тестовые данные в рабочую базу данных. В этом руководстве используется тот же метод, что и в тесте. Но в реальном приложении может потребоваться найти метод, проверяющий успешность обновления базы данных, не вводя тестовые данные в рабочую базу данных. В некоторых приложениях может быть целесообразно добавить что-то, а затем удалить.

Добавьте учащийся и просмотрите данные, введенные на странице **учащихся** , чтобы убедиться в возможности обновления данных в базе данных.

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

Проверьте правильность работы правил авторизации, выбрав пункт **Обновить кредиты** в меню **курсы** . Откроется страница **входа** . Введите учетные данные администратора, щелкните **войти**и отобразится страница **Обновление кредитов** .

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

Если вход выполнен успешно, отображается страница **Обновление кредитов** . Это означает, что база данных членства ASP.NET (с одной учетной записью администратора) успешно развернута.

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

Вы успешно развернули и протестировали сайт, и доступ к нему открыт через Интернет.

## <a name="creating-a-more-reliable-test-environment"></a>Создание более надежной тестовой среды

Как описано в руководстве по [развертыванию в тестовой среде](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) , самая надежная тестовая среда будет второй учетной записью на поставщике услуг размещения, которая аналогична рабочей учетной записи. Это было бы более затратно, чем использование локальных служб IIS в качестве тестовой среды, так как вам пришлось бы зарегистрировать вторую учетную запись размещения. Но если это предотвращает ошибки или сбои рабочего сайта, вы можете решить, что это стоит делать.

Большая часть процесса создания и развертывания в тестовой учетной записи похожа на то, что вы уже сделали для развертывания в рабочей среде.

- Создайте файл преобразования *Web. config* .
- Создайте учетную запись на поставщике услуг размещения.
- Создайте новый профиль публикации и разверните его для тестовой учетной записи.

### <a name="preventing-public-access-to-the-test-site"></a>Запрет общего доступа к тестовому сайту

Важное замечание для тестовой учетной записи заключается в том, что она будет находиться в Интернете, но вы не хотите, чтобы она использовалась. Для сохранения личного сайта можно использовать один или несколько следующих методов.

- Обратитесь к поставщику услуг размещения, чтобы задать правила брандмауэра, которые разрешают доступ к проверочному сайту только с IP-адресов, используемых для тестирования.
- Маскировка URL-адреса таким образом, чтобы он не был похож на URL-адрес общедоступного сайта.
- Используйте файл *robots. txt* , чтобы гарантировать, что поисковые системы не будут выполнять обход содержимого тестового сайта и передавать ссылки на него в результатах поиска.

Первый из этих методов, очевидно, является наиболее безопасным, но процедура для этого характерна для каждого поставщика услуг размещения и не будет рассмотрена в этом учебнике. Если вы размещаете поставщика услуг размещения, чтобы разрешить только вашему IP-адресу просматривать URL-адрес тестовой учетной записи, теоретически не нужно беспокоиться о его обходе. Но даже в этом случае развертывание файла *robots. txt* является хорошей идеей в качестве резервной копии на случай случайного выключения правила брандмауэра.

Файл *robots. txt* находится в папке проекта и должен содержать в нем следующий текст:

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

`User-agent` строка указывает поисковым системам, что правила в файле применяются ко всем поисковым средствам поисковой системы (роботы), а строка `Disallow` указывает, что обход страниц на сайте не должен выполняться.

Вы, вероятно, хотите, чтобы поисковые системы были в каталоге рабочего сайта, поэтому необходимо исключить этот файл из рабочего развертывания. Для этого см. статью **можно ли исключить определенные файлы или папки из развертывания?** в разделе [часто задаваемые вопросы о развертывании проекта веб-приложения ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment). Убедитесь, что исключение указывается только для профиля публикации в рабочей среде.

Создание второй учетной записи размещения является подходом к работе с тестовой средой, которая не является обязательной, но может быть, к добавлению затрат. В следующих учебниках вы продолжите использовать службы IIS в качестве тестовой среды.

В следующем руководстве вы обновите код приложения и развернете изменения в тестовой и рабочей средах.

> [!div class="step-by-step"]
> [Назад](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [Вперед](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
