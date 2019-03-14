---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: Веб-развертывание ASP.NET с помощью Visual Studio. Развертывание в рабочей среде | Документация Майкрософт
author: tdykstra
description: В этой серии руководств показано, как развернуть ASP.NET (публикации) веб-приложения, веб-приложениях службы приложений Azure или у стороннего поставщика размещения, Пол...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: f71d8311cbb1131d9c30c0bd9071a1c6c90f9976
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045851"
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>Веб-развертывание ASP.NET с помощью Visual Studio. Развертывание в рабочей среде
====================
по [том Дайкстра](https://github.com/tdykstra)

[Загрузите начальный проект](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> В этой серии руководств показано, как развернуть ASP.NET (публикации) веб-приложения для веб-приложениях службы приложений Azure или стороннего поставщика услуг размещения, с помощью Visual Studio 2012 или Visual Studio 2010. Сведения об этой серии см. в разделе [в первом учебнике серии](introduction.md).


## <a name="overview"></a>Обзор

В этом руководстве описано настроить учетную запись Microsoft Azure, создавать промежуточной и рабочей среды и развертывания в промежуточном веб-приложения ASP.NET и рабочих сред с помощью Visual Studio одним щелчком публикации компонентов.

При желании можно развернуть для стороннего поставщика услуг размещения. Большая часть процедуры, описанные в этом руководстве одинаковы для поставщика услуг размещения или Azure, за исключением того, что каждый поставщик имеет свой собственный пользовательский интерфейс для управления учетной записью и веб-сайта. Можно найти поставщика услуг размещения в [коллекции поставщиков](https://www.microsoft.com/web/hosting) веб-сайте Microsoft.com.

Напоминание. Если вы получаете сообщение об ошибке, или что-то не работает, как работать с руководством, обязательно обратитесь к странице "Устранение неполадок" в этой серии руководств.

## <a name="get-a-microsoft-azure-account"></a>Получить учетную запись Microsoft Azure

Если у вас нет учетной записи Azure, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [бесплатной пробной версии Azure](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

## <a name="create-a-staging-environment"></a>Создать промежуточную среду

> [!NOTE]
> Так как этот учебник написан, службе приложений Azure добавлена новая возможность, чтобы автоматизировать многие процессы для создания промежуточной и рабочей сред. См. в разделе [Настройка промежуточных сред для веб-приложений в службе приложений Azure](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/).


Как описано в [развертывание в этом руководстве тестовая среда,](deploying-to-iis.md), наиболее надежный тестовой среды — это узел, у поставщика услуг размещения, как рабочем веб-узле. Во многих поставщиков услуг размещения необходимо взвесить преимущества этого значительные дополнительные затраты, но в Azure можно создать Дополнительные бесплатные веб-приложение в качестве промежуточного приложения. Требуется база данных, и для этого дополнительные расходы за расходы на рабочую базу данных будет либо none или минимальным. В Azure вы платите объема хранилища базы данных, которые используются, а не для каждой базы данных, и объем дополнительного хранилища, которые будут использоваться в промежуточной среде будет минимальным.

Как описано в [развертывание в тестовой среде руководства](deploying-to-iis.md), в промежуточной и рабочей средах, которые вы собираетесь развернуть двух баз данных в одной базе данных. Если вы хотите хранить их отдельно, этот процесс будет таким же, за исключением того, что необходимо создать дополнительную базу данных для каждой среды и выбирается строка правильного назначения для каждой базы данных при создании профиля публикации.

В этом разделе руководства вы создадите веб-приложения и базы данных для промежуточной среды, и вы в промежуточную и тестирования существует, перед созданием и развертыванием в производственной среде.

> [!NOTE]
> Ниже показано, как создать веб-приложения в службе приложений Azure с помощью портала управления Azure. В последней версии пакета Azure SDK это можно также сделать не выходя из Visual Studio с помощью обозревателя сервера. В Visual Studio 2013 можно также создать непосредственно из диалогового окна публикации веб-приложения. Дополнительные сведения см. в разделе [создать веб-приложение ASP.NET в службе приложений Azure.](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)


1. В [портала управления Azure](https://manage.windowsazure.com/), нажмите кнопку **веб-сайтов**, а затем нажмите кнопку **New**.
2. Нажмите кнопку **веб-сайт**, а затем нажмите кнопку **настраиваемое создание**.

    **Новый веб-узел — настраиваемое создание** откроется мастер. **Настраиваемое создание** мастер позволяет создавать веб-сайта и базы данных, в то же время.
3. В **создать веб-сайт** шаг мастера введите строку в **URL-адрес** поле для использования в качестве уникального URL-адреса для вашего приложения в промежуточной среде. Например введите ContosoUniversity-staging123 (включая случайных чисел в конце, чтобы сделать его уникальным в случае, если берется ContosoUniversity промежуточной).

    Полный URL-адрес будет состоять из введенной здесь, а также суффикса, который отображается рядом с текстовым полем.
4. В **регион** раскрывающемся списке выберите регион, ближайший к вам.

    Этот параметр указывает, какой веб-приложения будет выполняться в центр обработки данных.
5. В **базы данных** раскрывающегося списка выберите **создать новую базу данных SQL**.
6. В **имя строки подключения DB** оставьте значение по умолчанию, *DefaultConnection*.
7. Щелкните стрелку, указывающую справа в нижней части окна.

    На следующем рисунке показано **создать веб-сайт** диалоговое окно с примеры значений в нем. URL-адрес и регион, который вы ввели будет отличаться.

    ![Создание веб-сайт](deploying-to-production/_static/image1.png)

    В мастере открывается **указать параметры базы данных** шаг.
8. В **имя** введите *ContosoUniversity* плюс случайное число, чтобы сделать уникальным, например *ContosoUniversity123*.
9. В **Server** выберите **новый сервер базы данных SQL**.
10. Введите имя и пароль администратора.

    Не используйте имеющиеся имя и пароль. Введите новое имя и пароль, который вы определяете для последующего использования при доступе к базе данных.
11. В **регион** выберите том же регионе, выбранном для веб-приложения.

    Веб-сервер и сервер базы данных в одном регионе обеспечивает наилучшую производительность и сокращает расходы.
12. Установите флажок в нижней части флажок, который подтверждает, что Вы завершили.

    На следующем рисунке показано **указать параметры базы данных** диалоговое окно с примеры значений в нем. Значения, которые вы ввели может отличаться.

    ![Шаг настройки базы данных веб-сайта New - создание с помощью мастера базы данных](deploying-to-production/_static/image2.png)

    Портал управления возвращает на страницу веб-сайтов и **состояние** столбец показывает, что создается веб-приложения. Через некоторое время (обычно это занимает меньше минуты) **состояние** столбец показывает, что веб-приложение успешно создано. На панели навигации слева, число веб-приложений, у вас есть в вашей учетной записи отображается рядом с полем **веб-сайтов** значок, а также количество баз данных отображается рядом с полем **баз данных SQL** значок.

    ![Веб-сайтов странице портала управления, созданные веб-сайта](deploying-to-production/_static/image3.png)

    Имя вашего веб-приложения будет отличаться от примера приложения на рисунке.

## <a name="deploy-the-application-to-staging"></a>Развертывание приложения в промежуточную среду

Теперь, когда вы создали веб-приложения и базы данных для промежуточной среды, чтобы его можно развернуть проект.

> [!NOTE]
> Эти инструкции показано, как создать профиль публикации, загрузив *.publishsettings* файл, который работает не только для Azure но и для независимых поставщиков услуг размещения. Последнюю версию пакета SDK для Azure также позволяет напрямую подключаться к Azure из Visual Studio и выберите из списка веб-приложений, которые имеются в вашей учетной записи Azure. В Visual Studio 2013, вы можете войти Azure из **веб-публикация** диалоговое окно или из **обозревателя серверов** окна. Дополнительные сведения см. в разделе [создать веб-приложение ASP.NET в службе приложений Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).


### <a name="download-the-publishsettings-file"></a>Загрузите файл PUBLISHSETTINGS

1. Щелкните имя веб-приложение, которое вы только что создали.

    ![Выберите сайт, чтобы перейти к панели мониторинга](deploying-to-production/_static/image4.png)
2. В разделе **быстрый обзор** в **панели мониторинга** щелкните **загрузить профиль публикации**.

    ![Профиль публикации ссылка для скачивания](deploying-to-production/_static/image5.png)

    Этот шаг загружает файл, содержащий все параметры, необходимые для развертывания приложения в веб-приложения. Вы импортируете этот файл в Visual Studio, поэтому не нужно вручную ввести соответствующую информацию.
3. Сохранить *.publishsettings* файл в папке, которую можно получить из Visual Studio.

    ![Сохранение файла PUBLISHSETTINGS](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > Безопасность — *.publishsettings* файл содержит учетные данные (Незакодированные), которые используются для управления подписками Azure и службами. Безопасность для этого файла рекомендуется временно хранить его за пределами исходных каталогов (например, в папке Libraries\Documents), а затем удалять после завершения импорта. Пользователь-злоумышленник, получивший доступ к *.publishsettings* файла можно изменить, создавать и удалять ваши службы Azure.

### <a name="create-a-publish-profile"></a>Создать профиль публикации

1. В Visual Studio щелкните правой кнопкой мыши проект ContosoUniversity в **обозревателе решений** и выберите **публикации** в контекстном меню.

    **Веб-публикации** откроется мастер.
2. Нажмите кнопку **профиль** вкладки.
3. Нажмите кнопку **Импортировать**.
4. Перейдите к *.publishsettings* загруженный ранее файл, а затем нажмите кнопку **откройте**.

    ![Диалоговое окно импорта параметров публикации](deploying-to-production/_static/image7.png)
5. В **подключения** щелкните **проверить подключение** чтобы убедиться в том, что параметры заданы правильно.

    После проверки подключения зеленая галочка отображается рядом с полем **проверить подключение** кнопки.

    Для некоторых поставщиков услуг размещения, при нажатии кнопки **проверить подключение**, может появиться **сообщение об ошибке сертификата** диалоговое окно. В противном случае убедитесь, что имя сервера как ожидалось. Если имя сервера указано правильно, выберите **сохранить этот сертификат для будущих сеансов Visual Studio** и нажмите кнопку **Accept**. (Эта ошибка означает, что избежать затрат на приобретение SSL-сертификат для URL-адрес, который вы развертываете выбрал поставщика услуг размещения. Если вы предпочитаете установить безопасное подключение с использованием действительного сертификата, обратитесь к поставщику услуг размещения.)
6. Нажмите кнопку **Далее**.

    ![значок успешного подключения и кнопка "Далее" на вкладке "Подключение"](deploying-to-production/_static/image8.png)
7. В **параметры** вкладке, разверните узел **параметры публикации файлов**, а затем выберите **исключить файлы из приложения\_папка данных**.

    Сведения о других параметрах в разделе **параметры публикации файлов**, см. в разделе [развертывание в IIS](deploying-to-iis.md) руководства. На снимке экрана, время отображается результат этого шага и следующие действия по настройке базы данных — в конце действия по настройке базы данных.
8. В разделе **DefaultConnection** в **баз данных** настройте развертывания базы данных для базы данных членства.
9. 1. Выберите **обновления базы данных**.

        **Строку подключения к удаленному** поле непосредственно под **DefaultConnection** заполняется строку подключения из файла .publishsettings. Строка подключения содержит учетные данные SQL Server, которые хранятся в виде обычного текста в *.pubxml* файла. Если вы предпочитаете не храните их там без возможности восстановления, можно удалить их из профиля публикации после развертывания базы данных и хранить их в Azure. Дополнительные сведения см. в разделе [как защитить базы данных ASP.NET строки подключения при развертывании в Azure из источника](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) в блоге Скотта Хансельмана.
      2. Нажмите кнопку **настроить обновление базы данных**.
      3. В **Настройка обновления базы данных** диалоговом окне щелкните **добавить скрипт SQL**.
      4. В **добавить скрипт SQL** поле, перейдите в каталог *aspnet-data-prod.sql* скрипт, сохраненный ранее в папке решения, а затем нажмите кнопку **откройте**.
      5. Закрыть **Настройка обновления базы данных** диалоговое окно.
10. В разделе **SchoolContext** в **баз данных** выберите **выполнить Code First Migrations (при запуске приложения)**.

    Visual Studio отображает **выполнить Code First Migrations** вместо **обновления базы данных** для `DbContext` классы. Если вы хотите использовать поставщик dbDacFx вместо миграции для развертывания базы данных, доступный с помощью `DbContext` , представлена в разделе [как развернуть базу данных Code First без миграции?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) в часто задаваемых вопросов развертывания Web для Visual Studio и ASP.NET на сайте MSDN.

    **Параметры** вкладке теперь выглядит как в следующем примере:

    ![Параметры вкладки для промежуточного хранения](deploying-to-production/_static/image9.png)
11. Выполните следующие действия, чтобы сохранить профиль и переименуйте его в *промежуточной*:

    1. Нажмите кнопку **профиль** , а затем щелкните **Управление профилями**.
    2. Импорт созданы два новых профиля, для FTP и один для веб-развертывания. Вы настроили профиль веб-развертывания: переименовать этот профиль для *промежуточной*.

        ![Переименовать профиль подготовки](deploying-to-production/_static/image10.png)
    3. Закрыть **изменить профили публикации Web** диалоговое окно.
    4. Закрыть **веб-публикации** мастера.

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>Настройка преобразования профиля публикации для индикатора среды

> [!NOTE]
> В этом разделе показано, как настроить преобразование Web.config для индикатора среды. Поскольку индикатор располагается в `<appSettings>` элемент, у вас есть другой способ для указания преобразование при развертывании в службе приложений Azure. Дополнительные сведения см. в разделе [Web.config, указав параметры в Azure](web-config-transformations.md#watransforms).


1. В **обозревателе решений**, разверните **свойства**, а затем разверните **PublishProfiles**.
2. Щелкните правой кнопкой мыши *Staging.pubxml*, а затем нажмите кнопку **добавить преобразования конфигурации**.

    ![Добавить преобразование конфигурации для промежуточного хранения](deploying-to-production/_static/image11.png)

    Visual Studio создает *Web.Staging.config* файла преобразования и открывает его.
3. В *Web.Staging.config* файл преобразования, вставьте следующий код сразу же после открытия `configuration` тега.

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    При использовании профиля публикации для промежуточного хранения, это преобразование задает индикатор среды «Prod». В развернутой веб-приложение вы не увидите любые суффиксы, такие как «(Dev)» или «(тест)» после заголовок H1 «Contoso University».
4. Щелкните правой кнопкой мыши *Web.Staging.config* файл и нажмите кнопку **преобразования предварительной версии** чтобы убедиться в том, что преобразование коде создает необходимые изменения.

    **Web.config предварительной версии** окна показан результат применения обоих *Web.Release.config* преобразует и *Web.Staging.config* преобразования.

### <a name="prevent-public-use-of-the-test-app"></a>Запретить использование общих тестирование приложения

Особенно важно для промежуточного приложения — что оно станет доступно в Интернете, но вы не хотите пользоваться его. Чтобы свести к минимуму вероятность того, что люди будет находить и использовать его, можно использовать один или несколько из следующих методов:

- Установить правила брандмауэра, разрешающие доступ для промежуточного приложения только из IP-адреса, используемые для тестирования, промежуточного хранения.
- Используйте допустимого URL-адреса, который может быть организовано угадать.
- Создание *robots.txt* убедитесь, что поисковые системы не будет обходить ссылок приложения и отчет теста к нему в результатах поиска.

Первый из этих методов является наиболее эффективным, но не рассматривается в этом руководстве, поскольку потребуется развернуть в Azure облачную службу вместо службы приложений Azure. Дополнительные сведения об облачных службах и ограничения IP-адресов в Azure, см. в разделе [вычислений размещения, предоставляемые Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) и [блок определенных IP-адресов доступ к веб-роли](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx). Если вы развертываете стороннего поставщика услуг размещения, обратитесь к поставщику, чтобы узнать, как реализовать ограничения IP-адресов.

В этом руководстве вы создадите *robots.txt* файл.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект ContosoUniversity и нажмите кнопку **Добавление нового элемента**.
2. Создайте новый **текстовый файл** с именем *robots.txt*и поместить в нее следующий текст:

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent` Укажет поисковых систем, в файле правила применяются ко всем web обходчикам (роботов), и `Disallow` строка указывает, что следует выполнить обход нет страниц на сайте.

    Вы хотите поисковыми каталога рабочего приложения, поэтому необходимо исключить этот файл из развертывания в рабочей среде. Для выполнения, что вы настроите профиль публикации параметр в рабочей среде, при ее создании.

### <a name="deploy-to-staging"></a>Развертывание в промежуточное хранилище

1. Откройте **веб-публикации** мастера, щелкнув правой кнопкой мыши проект университета Contoso команду **публикации**.
2. Убедитесь, что **промежуточной** выбран профиль.
3. Нажмите кнопку **Опубликовать**.

    **Вывода** окно показывает, какие действия по развертыванию были выполнены и передает об успешном завершении развертывания. URL-адрес развернутого веб-приложения автоматически откроется браузер по умолчанию.

## <a name="test-in-the-staging-environment"></a>Тестирование в промежуточной среде

Обратите внимание на то, что среда отсутствует (отсутствует» (тест)» или «(Dev)» после заголовком H1, который показывает, что *Web.config* выполнено преобразование для индикатора среды.

![Домашняя страница промежуточного хранения](deploying-to-production/_static/image12.png)

Запустите **учащихся** страницу, чтобы убедиться, что развернутая база данных имеет не учащихся.

Запустите **преподавателей** страницу, чтобы убедиться, что Code First заполнена начальными значениями базу данных данными преподавателя:

Выберите **добавить учащихся** из **учащихся** меню, добавить учащихся, а затем просмотрите нового учащегося в **учащихся** страницу, чтобы убедиться, что вы можете успешно записи в базу данных .

Из **курсы** щелкните **обновления кредиты**. **Кредиты обновления** страницы требуются права администратора, поэтому **вход** откроется страница. Введите учетные данные учетной записи администратора, что вы создали ранее («admin» и «prodpwd»). **Обновления кредиты** отображается страница, которая проверяет, что учетную запись администратора, созданную в предыдущем учебном курсе был правильно развернут в тестовую среду.

Запрос недопустимый URL-адрес ошибки, отслеживать ELMAH и затем запросить ELMAH отчет об ошибке. Если вы развертываете стороннего поставщика услуг размещения, можно обнаружить отчета является пустым по той же причине, в который он был пустым в предыдущем учебном курсе. Будет необходимо использовать средства управления поставщика услуг размещения учетной записи, чтобы настроить разрешения для папки для включения ELMAH для записи в папке журнала.

Созданное приложение теперь работает в облаке как веб-приложение, так же, как вы будете использовать его для рабочей среды. Так как все работает правильно, следующим шагом является развертывание в рабочей среде.

## <a name="deploy-to-production"></a>Развертывание в рабочей среде

Процесс создания рабочего веб-приложения и развертывания в рабочей среде аналогичен промежуточного хранения, за исключением того, что вам нужно исключить *robots.txt* из развертывания. Для этого требуется изменить файл профиля публикации.

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>Создание рабочей среды и профиль публикации в рабочей среде

1. Создание рабочего веб-приложения и базы данных в Azure, выполнив ту же процедуру, которая использовалась для промежуточного хранения.

    При создании базы данных, можно перевести его на том же сервере, созданную ранее, или создать новый сервер.
2. Скачайте *.publishsettings* файла.
3. Создать профиль публикации, импортировав производства *.publishsettings* файл, выполнив ту же процедуру, которая использовалась для промежуточного хранения.

    Не забудьте настроить сценарий развертывания данных с использованием **DefaultConnection** в **баз данных** раздел **параметры** вкладки.
4. Переименовать профиль публикации, *рабочей*.
5. Настройка преобразования профиля публикации для индикатора среды, выполнив ту же процедуру, которая использовалась для промежуточного хранения...

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>Изменить pubxml-файл, чтобы исключить robots.txt

Имена файлов имеют профиль публикации &lt;profilename&gt;*.pubxml* и находятся в папке *PublishProfiles* папки. *PublishProfiles* осуществляется в папку *свойства* проекта папку веб-приложения C#, в разделе *Мой проект* папки в проект VB веб-приложения или в разделе *Приложения\_данных* папки в проект веб-приложения. Каждый *.pubxml* файл содержит параметры, которые применяются к одному профиль публикации. В этих файлах хранятся значения, введенные в мастере публикации веб-сайта, и их можно создать или изменить параметры, которые не являются доступными в пользовательском Интерфейсе Visual Studio можно изменять.

По умолчанию *.pubxml* файлы будут включены в проект при создании профиля публикации, но их можно исключить из проекта Visual Studio по-прежнему будет использовать их. Visual Studio просматривает *PublishProfiles* папку для *.pubxml* файлы, независимо от того, включены ли они в проекте.

Для каждого *.pubxml* файла есть *. pubxml.user* файл. *. Pubxml.user* файл содержит зашифрованный пароль, если вы выбрали **сохранить пароль** параметр и по умолчанию, он исключается из проекта.

Объект *.pubxml* файл содержит параметры, относящиеся к профиля определенной публикации. Если вы хотите настроить параметры, которые применяются ко всем профилям, можно создать *. wpp.targets* файл. Процесс построения импортирует эти файлы в *.csproj* или *.vbproj* файл проекта, поэтому большинство параметров, которые можно настроить в файле проекта может быть настроена в этих файлах. Дополнительные сведения о *.pubxml* файлы и *. wpp.targets* файлы, см. в разделе [как: Изменять параметры развертывания в публикации (.pubxml) профиля файлов и. WPP.targets в веб-проектов Visual Studio](https://msdn.microsoft.com/library/ff398069.aspx).

1. В **обозревателе решений**, разверните **свойства** и разверните **PublishProfiles**.
2. Щелкните правой кнопкой мыши *Production.pubxml* и нажмите кнопку **откройте**.

    ![Откройте pubxml-файл](deploying-to-production/_static/image13.png)
3. Щелкните правой кнопкой мыши *Production.pubxml* и нажмите кнопку **откройте**.
4. Добавьте следующие строки непосредственно перед закрывающим `PropertyGroup` элемент:

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    Pubxml-файл теперь выглядит как в следующем примере:

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    Дополнительные сведения о том, как исключить файлы и папки, см. в разделе [можно ли исключить определенные файлы или папки из развертывания?](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) в **часто задаваемые вопросы развертывания Web для Visual Studio и ASP.NET** на сайте MSDN.

### <a name="deploy-to-production"></a>Развертывание в рабочей среде

1. Откройте **веб-публикации** мастера убедитесь, что **рабочей** профиль публикации выбран, а затем нажмите кнопку **начать просмотр** на **предварительной версии**вкладку, чтобы убедиться, что *robots.txt* файла не копируются в рабочем приложении.

    ![Просмотр файлов, которые будут публиковаться в рабочей среде](deploying-to-production/_static/image14.png)

    Просмотрите список файлов, которые будут скопированы. Как мы видим, все *.cs* файлов, включая *. aspx.cs*, *. aspx.designer.cs*, *Master.cs*, и  *Master.Designer.cs* файлы пропускаются. Весь этот код был скомпилирован в *ContosoUniversity.dll* и *ContosUniversity.pdb* файлы, которые вы найдете в *bin* папки. Так как только *.dll* необходим для выполнения приложения и указанный ранее должны развертываться только файлы, необходимые для запуска приложения, то никакие *.cs* файлы были скопированы в место назначения Среда. *Obj* папки и *ContosoUniversity.csproj* и *. csproj.user* файлы пропускаются по той же причине.

    Нажмите кнопку **публикации** для развертывания в рабочей среде.
2. Тестирование в рабочей среде, выполнив ту же процедуру, которая использовалась для промежуточного хранения.

    Все, что идентична промежуточного хранения, за исключением URL-адрес и отсутствие *robots.txt* файл.

## <a name="summary"></a>Сводка

Вы успешно развернуть и протестировать веб-приложения, и он доступен публично через Интернет.

![Домашняя страница рабочей среде](deploying-to-production/_static/image15.png)

В следующем руководстве вы обновите код приложения и развертывание изменений в средах тестирования, промежуточной и рабочей.

> [!NOTE]
> Когда приложение используется в рабочей среде следует реализацию плана восстановления. То есть вы должны периодически резервное копирование баз данных из рабочего приложения в место безопасного хранения и должен обеспечить такие резервные копии нескольких поколений ОС. При обновлении базы данных, следует создайте резервную копию из непосредственно перед изменением. Затем Если вы сделаете ошибку и не обнаружит его до, после его развертывания в рабочей среде, по-прежнему можно восстановить базу данных к состоянию, в котором он находился перед его был поврежден. Дополнительные сведения см. в разделе [резервной копии базы данных SQL Azure и восстановление](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx).
> 
> 
> [!NOTE]
> В этом руководстве SQL Server edition, который вы развертываете — база данных SQL Azure. Во время процесса развертывания похожа на другие выпуски SQL Server, приложение реальной рабочей среде может потребоваться специального кода для базы данных SQL Azure в некоторых сценариях. Дополнительные сведения см. в разделе [работу с базой данных SQL Azure](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) и [Выбор между SQL Server и базы данных SQL Azure](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing).
> 
> [!div class="step-by-step"]
> [Назад](setting-folder-permissions.md)
> [Вперед](deploying-a-code-update.md)