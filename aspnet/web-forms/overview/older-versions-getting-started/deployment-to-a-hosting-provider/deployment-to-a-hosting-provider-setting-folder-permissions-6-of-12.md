---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 'Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: Настройка разрешений для папки — 6 из 12 | Документация Майкрософт'
author: tdykstra
description: В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 85a77a196cf3458bbb2e6308838a846936cd070b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633538"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: Настройка разрешений для папки — 6 из 12

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web. При установке обновления веб-публикации можно также использовать Visual Studio 2010. Введение в серию см. [в первом учебнике серии](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Руководство, в котором показаны функции развертывания, появившиеся после выпуска версии-КАНДИДАТа Visual Studio 2012, демонстрирует развертывание SQL Server выпусков, отличных от SQL Server Compact, и демонстрация развертывания в веб-приложениях службы приложений Azure см. в разделе [ASP.NET Web Deploying using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Обзор

В этом руководстве вы задаете разрешения для папки *ELMAH* на развернутом веб-сайте, чтобы приложение могла создавать файлы журналов в этой папке.

При тестировании веб-приложения в Visual Studio с помощью Visual Studio Development Server (Cassini) приложение выполняется под вашим удостоверением. Вы, скорее всего, являетесь администратором на компьютере разработчика и имеете полный доступ к любому файлу в любой папке. Но если приложение выполняется в службах IIS, оно выполняется под удостоверением, определенным для пула приложений, которому назначен сайт. Обычно это определяемая системой учетная запись с ограниченными разрешениями. По умолчанию он имеет разрешения на чтение и выполнение для файлов и папок вашего веб-приложения, но у него нет доступа на запись.

Это становится проблемой, если приложение создает или обновляет файлы, что является общей потребностью в веб-приложениях. В приложении университета Contoso ELMAH создает XML-файлы в папке *ELMAH* , чтобы сохранить сведения об ошибках. Даже если вы не используете что-либо вроде ELMAH, ваш сайт может позволить пользователям отправлять файлы или выполнять другие задачи, которые записывают данные в папку на сайте.

Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="testing-error-logging-and-reporting"></a>Тестирование ведения журнала ошибок и отчетов

Чтобы увидеть, как приложение работает неправильно в службах IIS (хотя это было сделано при тестировании в Visual Studio), можно вызвать ошибку, которая обычно заносится в журнал ELMAH, а затем открыть в журнале ошибок ELMAH, чтобы просмотреть подробные сведения. Если ELMAH не удалось создать XML-файл и сохранить сведения об ошибке, отобразится пустой отчет об ошибках.

Откройте браузер и перейдите в `http://localhost/ContosoUniversity`, а затем запросите недопустимый URL-адрес, например *студентскскскс. aspx*. Вместо страницы *женерицеррорпаже. aspx* отображается созданная системой страница ошибки, так как параметр `customErrors` в файле Web. config имеет значение "RemoteOnly" и локально выполняются службы IIS:

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

Теперь запустите *ELMAH. axd* , чтобы просмотреть отчет об ошибках. Появится пустая страница журнала ошибок, так как ELMAH не удалось создать XML-файл в папке *ELMAH* :

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>Установка разрешения на запись в папку ELMAH

Разрешения для папки можно задать вручную или сделать автоматически частью процесса развертывания. Чтобы сделать его автоматическим, требуется сложный код MSBuild, и так как это необходимо сделать только при первом развертывании, в этом учебнике показано только, как сделать это вручную. (Сведения о том, как сделать эту часть процесса развертывания, см. в разделе [Установка разрешений папки для веб-публикации](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) в блоге Саид Хашими.)

В **проводнике Windows**перейдите по адресу *к:\инетпуб\ввврут\контосауниверсити*. Щелкните правой кнопкой мыши папку *ELMAH* , выберите пункт **свойства**, а затем перейдите на вкладку **Безопасность** .

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

(Если вы не видите **DefaultAppPool** в списке **имен групп или пользователей** , вероятно, вы использовали другой метод, отличный от указанного в этом руководстве, для настройки IIS и ASP.NET 4 на компьютере. В этом случае выясните, какое удостоверение используется пулом приложений, назначенным приложению университета Contoso, и предоставьте ему разрешение на запись. См. ссылки о удостоверениях пула приложений в конце этого руководства.)

Нажмите кнопку **Правка**. В диалоговом окне **разрешения для ELMAH** выберите **DefaultAppPool**, а затем установите флажок **записать** в столбце **Разрешить** .

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

Нажмите кнопку **ОК** в обоих диалоговых окнах.

## <a name="retesting-error-logging-and-reporting"></a>Повторное тестирование ведения журнала ошибок и отчетов

Протестируйте, вызывая ошибку повторно тем же способом (запросите неверный URL-адрес) и запустите страницу **журнал ошибок** . На этот раз ошибка появляется на странице.

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

Кроме того, необходимо разрешение на запись в папку *данных приложения\_* , так как в этой папке есть SQL Server Compact файлы базы данных и необходимо иметь возможность обновлять данные в этих базах данных. Однако в этом случае вам не нужно предпринимать дополнительных действий, так как процесс развертывания автоматически устанавливает разрешение на запись в папку *приложения\_данных* .

Вы выполнили все задачи, необходимые для правильной работы университета Contoso в службах IIS на локальном компьютере. В следующем руководстве вы сделаете сайт общедоступным, развернув его для поставщика услуг размещения.

## <a name="more-information"></a>Дополнительные сведения

В этом примере, причина, по которой ELMAH не удалось сохранить файлы журнала, достаточно очевидна. Трассировку IIS можно использовать в случаях, когда причина проблемы не настолько очевидна; см. раздел [Устранение неполадок с неудачными запросами с помощью трассировки в IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) на сайте IIS.NET.

Дополнительные сведения о том, как предоставить разрешения удостоверениям пула приложений, см. в разделе [удостоверения пула приложений](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) и [Защита содержимого в IIS с помощью списков управления доступом файловой системы](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) на сайте IIS.NET.

> [!div class="step-by-step"]
> [Назад](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [Вперед](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
