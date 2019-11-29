---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание обновления только для кода — 8 из 12 | Документация Майкрософт'
author: tdykstra
description: В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/28/2019
ms.locfileid: "74572771"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a>Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio или Visual Web Developer: развертывание обновления только для кода — 8 из 12

от [Tom Dykstra)](https://github.com/tdykstra)

[Скачать начальный проект](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> В этой серии учебников показано, как развернуть (опубликовать) проект веб-приложения ASP.NET, включающий базу данных SQL Server Compact, с помощью Visual Studio 2012 RC или Visual Studio Express 2012 RC для Web. При установке обновления веб-публикации можно также использовать Visual Studio 2010. Введение в серию см. [в первом учебнике серии](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Руководство, в котором показаны функции развертывания, появившиеся после выпуска версии-КАНДИДАТа Visual Studio 2012, демонстрирует развертывание SQL Server выпусков, отличных от SQL Server Compact, и демонстрация развертывания в веб-приложениях службы приложений Azure см. в разделе [ASP.NET Web Deploying using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Обзор

После первоначального развертывания работа по обслуживанию и разработке веб-узла будет продолжена, и до тех пор, когда потребуется развернуть обновление. В этом руководстве описывается процесс развертывания обновления кода приложения. Это обновление не затрагивает изменение базы данных. в следующем руководстве вы увидите, что отличается от развертывания изменений базы данных.

Напоминание. Если вы получаете сообщение об ошибке или что-то не работает при работе с этим руководством, обязательно ознакомьтесь со [страницей устранения неполадок](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="making-a-code-change"></a>Внесение изменений в код

В качестве простого примера обновления для приложения вы добавите на страницу **инструкторов** список курсов, которые научились выбранному преподавателю.

Если вы запустили страницу **инструкторов** , то увидите, что в сетке есть ссылки **SELECT** , но они не выполняют никаких действий, чем сделать фон строки серым.

[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)

Теперь вы добавите код, который выполняется при нажатии ссылки **SELECT** и отображает список курсов, которые научились выбранному преподавателю.

В *инструкторах. aspx*добавьте следующую разметку сразу после элемента управления `Label` **еррормессажелабел** :

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

Запустите страницу и выберите лектора. Вы увидите список курсов, которые научились этим преподавателем.

[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)

## <a name="deploying-the-code-update-to-the-test-environment"></a>Развертывание обновления кода в тестовой среде

Развертывание в тестовой среде — это простая задача повторного выполнения публикации одним щелчком. Чтобы ускорить этот процесс, можно использовать панель инструментов **веб-публикация одним щелчком** .

В меню **вид** выберите **панели инструментов** , а затем выберите **веб-публикация одним щелчком**.

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

В **Обозреватель решений**выберите проект ContosoUniversity.

на панели инструментов **веб-публикация одним щелчком** выберите профиль **тестовой** публикации, а затем щелкните **Опубликовать веб-сайт** (значок со стрелками влево и вправо).

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

Visual Studio развертывает обновленное приложение, и браузер автоматически открывается на домашней странице. Запустите страницу инструкторы и выберите лектора, чтобы убедиться, что обновление успешно развернуто.

[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)

Обычно вы также выполняете регрессионное тестирование (то есть протестируйте остальную часть сайта, чтобы убедиться, что новое изменение не привело к нарушению существующих функций). Но в этом учебнике вы пропустите этот шаг и продолжите развертывание обновления в рабочей среде.

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a>Предотвращение повторного развертывания состояния начальной базы данных в рабочей среде

В реальном приложении пользователи взаимодействуют с рабочим сайтом после первоначального развертывания, а базы данных заполняются динамическими данными. Поэтому вы не хотите повторно развертывать базу данных членства в первоначальном состоянии, что приведет к очистке всех данных в реальном времени. Так как SQL Server Compact базы данных — это файлы в папке *данных приложения\_* , необходимо запретить это, изменив параметры развертывания, чтобы файлы в папке *данных приложения\_* не были развернуты.

Откройте окно **свойств проекта** для проекта ContosoUniversity и выберите вкладку **Упаковка и публикация веб-сайта** . Убедитесь, что в раскрывающемся **списке Конфигурация** выбрано значение **активно (выпуск)** или **выпуск** , выберите **исключить файлы из папки\_данных приложения**.

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

Если вы решили развернуть отладочную сборку в будущем, рекомендуется внести одно и то же изменение в конфигурацию отладочной сборки: изменить **конфигурацию** на **отладку** , а затем выбрать **исключить файлы из папки\_данных приложения**.

Сохраните и закройте вкладку **Пакет/Публикация веб-сайта** .

> [!NOTE] 
> 
> [!IMPORTANT]
> Убедитесь, что вы не **удалили дополнительные файлы в месте назначения** , выбранном в профилях публикации. Если выбрать этот параметр, то в процессе развертывания будут удалены базы данных, которые имеются в приложении\_данных на развернутом сайте, и будет удалена сама папка данных приложения\_.

## <a name="preventing-user-access-to-the-production-site-during-update"></a>Запрет доступа пользователей к рабочему сайту во время обновления

Изменение, которое вы развертываете, теперь является простым изменением одной страницы. Но иногда вы развертываете большие изменения, и в этом случае веб-узел может вести себя странно, если пользователь запрашивает страницу до завершения развертывания. Чтобы избежать этого, можно использовать *приложение\_автономном htm* файл. При помещении файла с именем *app\_offline. htm* в корневую папку приложения IIS автоматически отображает этот файл вместо запуска приложения. Чтобы предотвратить доступ во время развертывания, помещаете *приложение\_offline. htm* в корневую папку, запускает процесс развертывания, а затем удаляет *приложение\_offline. htm*.

В **Обозреватель решений**щелкните правой кнопкой мыши решение (не один из проектов) и выберите пункт **создать папку решения**.

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

Назовите папку *солутионфилес*.

В новой папке создайте HTML-страницу с именем *app\_offline. htm*. Замените существующее содержимое следующей разметкой:

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

Вы можете скопировать *приложение\_автономный htm* -файл на сайт с помощью FTP-соединения или служебной программы **диспетчера файлов** на панели управления поставщика услуг размещения. В этом руководстве используется **Диспетчер файлов**.

Откройте панель управления и выберите **Диспетчер файлов** , как описано в учебнике [развертывание в рабочей среде](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) . Выберите **contosouniversity.com** , а затем **wwwroot** , чтобы получить доступ к корневой папке приложения, а затем нажмите кнопку **Отправить**.

[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)

В диалоговом окне **Отправка файла** выберите *приложение\_автономный htm* файл и нажмите кнопку **Отправить**.

[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)

Перейдите по URL-адресу вашего сайта. Вы увидите, что теперь вместо домашней страницы отображается страница *приложение\_автономно. htm.*

[![App_offline. htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)

Теперь все готово для развертывания в рабочей среде.

## <a name="deploying-the-code-update-to-the-production-environment"></a>Развертывание обновления кода в рабочей среде

На панели инструментов **веб-публикация одним щелчком** выберите профиль **рабочей** публикации и нажмите кнопку **Опубликовать веб-сайт**.

Visual Studio развертывает обновленное приложение и открывает браузер на домашней странице сайта. Откроется *приложение\_автономный htm* -файл. Прежде чем можно будет проверить успешность развертывания, необходимо удалить *приложение\_автономный htm* -файл.

Вернитесь в приложение **диспетчера файлов** на панели управления. Выберите **contosouniversity.com** и **wwwroot**, выберите **приложение\_автономно. htm**, а затем нажмите кнопку **Удалить**.

[![Deleting_app_offline. htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)

В браузере откройте страницу инструкторы на общедоступном сайте и выберите лектора, чтобы проверить успешность развертывания обновления.

[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)

Теперь вы развернули обновление приложения, которое не затрагивает изменение базы данных. В следующем учебнике показано, как развернуть изменение базы данных.

> [!div class="step-by-step"]
> [Назад](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [Вперед](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
