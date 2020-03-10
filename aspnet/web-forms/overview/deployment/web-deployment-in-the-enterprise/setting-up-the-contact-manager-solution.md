---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Настройка решения диспетчера контактов | Документация Майкрософт
author: jrjlee
description: В этом разделе описывается загрузка и настройка решения диспетчера контактов для локального запуска на рабочей станции разработчика.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511164"
---
# <a name="setting-up-the-contact-manager-solution"></a>Настройка решения диспетчера контактов

кто [Джейсон Иванов](https://github.com/jrjlee)

[Скачать в формате PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> В этом разделе описывается загрузка и настройка решения диспетчера контактов для локального запуска на рабочей станции разработчика.

## <a name="system-requirements"></a>Требования к системе

Для локального запуска решения диспетчера контактов и выполнения других задач, описанных в этом руководстве, необходимо установить это программное обеспечение на рабочую станцию разработчика:

- Visual Studio 2010 с пакетом обновления 1 (SP1), Premium или Ultimate Edition
- Internet Information Services (IIS) 7.5 Express
- SQL Server Express 2008 R2
- Средство веб-развертывания IIS (веб-развертывание) 2,1 или более поздней версии
- ASP.NET 4,0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

За исключением Visual Studio 2010, вы можете скачать и установить последние версии всех этих продуктов и компонентов с помощью [установщика веб-платформы](https://go.microsoft.com/?linkid=9805118).

## <a name="download-and-extract-the-solution"></a>Скачивание и извлечение решения

Вы можете скачать пример приложения диспетчера контактов из коллекции кода MSDN [здесь](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).

## <a name="configure-and-run-the-solution"></a>Настройка и запуск решения

Чтобы настроить и запустить решение диспетчера контактов на локальном компьютере, необходимо выполнить следующие общие действия:

1. Если вы еще не сделали этого, создайте локальную базу данных служб приложений ASP.NET с включенными функциями управления членством и ролями.
2. Измените строки подключения в файлах *Web. config* , чтобы они указывали на локальный экземпляр SQL Server Express.
3. Запустите решение из Visual Studio 2010.

Оставшаяся часть этого раздела содержит дополнительные рекомендации по выполнению каждой из этих задач.

**Создание базы данных служб приложений**

1. Откройте командную строку Visual Studio 2010. Для этого в меню **Пуск** наведите указатель на пункт **все программы**, выберите **Microsoft Visual Studio 2010**, щелкните **инструменты Visual Studio**и выберите пункт **Командная строка Visual Studio (2010)** .
2. В командной строке введите следующую команду и нажмите клавишу ВВОД:

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. Используйте параметр **– C** , чтобы указать строку подключения для сервера базы данных.
    2. Используйте параметр **– A** , чтобы указать компоненты служб приложений, которые необходимо добавить в базу данных. В этом случае **m** указывает, что вы хотите добавить поддержку для поставщика членства, а **r** указывает, что вы хотите добавить поддержку для диспетчера ролей.
    3. Используйте параметр **– d** , чтобы указать имя для базы данных служб приложений. Если этот параметр не задан, программа создаст базу данных с именем по умолчанию **aspnetdb**.
3. После успешного создания базы данных в командной строке отобразится подтверждение.

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> Дополнительные сведения о служебной программе ASPNET\_регскл см. в статье [ASP.NET SQL Server Registration Tool (aspnet\_регскл. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).

Следующий шаг — убедиться, что строки подключения в точке решения диспетчера контактов указывают на локальный экземпляр SQL Server Express.

**Обновление строк подключения**

1. Откройте решение диспетчера контактов в Visual Studio 2010.
2. В окне **Обозреватель решений** разверните проект **ContactManager. MVC** , а затем дважды щелкните узел **Web. config** .

    > [!NOTE]
    > Проект ContactManager. MVC содержит два файла *Web. config* . Необходимо изменить файл уровня проекта.

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. Убедитесь, что в элементе **connectionStrings** строка подключения с именем **ApplicationServices** указывает на локальную базу данных служб приложений ASP.NET.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. В окне **Обозреватель решений** разверните проект **ContactManager. Service** , а затем дважды щелкните узел **Web. config** .

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. В элементе **connectionStrings** в строке подключения с именем **ContactManagerContext**убедитесь, что для свойства **источник данных** задан локальный экземпляр SQL Server Express. В строке подключения никаких других изменений не требуется.

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. Сохраните все открытые файлы.

Теперь вы можете запустить решение диспетчера контактов на локальном компьютере.

> [!NOTE]
> Если выполнить эти действия без предварительного создания базы данных служб приложений, ASP.NET создаст базу данных при первой попытке создать пользователя. Однако создание базы данных вручную обеспечивает гораздо больший контроль над набором функций служб приложений, которые требуется поддерживать.

**Запуск решения диспетчера контактов**

1. В Visual Studio 2010 нажмите клавишу F5.
2. Internet Explorer запустит и запросит URL-адрес приложения диспетчера контактов ASP.NET MVC 3. По умолчанию приложение отображает страницу **все контакты** .

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. Добавьте несколько контактов, а затем убедитесь, что приложение работает должным образом.

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. Перейдите к `http://localhost:50114/Account/Register` (измените URL-адрес, если приложение размещено на другом порте). Добавьте имя пользователя, адрес электронной почты и пароль и убедитесь, что вы можете успешно зарегистрировать учетную запись.

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. Перейдите к `http://localhost:50114/Account/LogOn` (измените URL-адрес, если приложение размещено на другом порте). Убедитесь, что вы можете войти в систему, используя только что созданную учетную запись.

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. Закройте Internet Explorer, чтобы завершить отладку.

## <a name="conclusion"></a>Заключение

На этом этапе решение диспетчера контактов должно быть полностью настроено для запуска на локальном компьютере. Решение можно использовать в качестве ссылки при работе с другими подразделами этого учебника.

В следующем разделе, посвященном [файлу проекта](understanding-the-project-file.md), объясняется, как можно использовать пользовательские файлы проекта Microsoft Build Engine (MSBuild) в решении диспетчера контактов для управления процессом развертывания.

> [!div class="step-by-step"]
> [Назад](the-contact-manager-solution.md)
> [Вперед](understanding-the-project-file.md)
