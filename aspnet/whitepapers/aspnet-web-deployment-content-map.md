---
uid: whitepapers/aspnet-web-deployment-content-map
title: Веб-развертывание ASP.NET — Рекомендуемые ресурсы | Документация Майкрософт
author: rick-anderson
description: В этом разделе приведены ссылки на документацию по развертыванию (публикации) веб-приложений ASP.NET в службах IIS с помощью Visual Studio 2010, Visual Web de...
ms.author: riande
ms.date: 03/14/2014
ms.assetid: 58b583cd-c4ab-47a3-8527-8c92c298c91f
msc.legacyurl: /whitepapers/aspnet-web-deployment-content-map
msc.type: content
ms.openlocfilehash: 96873c8f2b0ad2415f371aceb651400c801a3338
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517278"
---
# <a name="aspnet-web-deployment---recommended-resources"></a>Веб-развертывание в ASP.NET. Рекомендуемые ресурсы

> В этом разделе приведены ссылки на документацию по развертыванию (публикации) веб-приложений ASP.NET в службах IIS с помощью Visual Studio 2010, Visual Web Developer 2010 и более поздних версий.
> 
> Если вы знакомы с отличной записью блога, потоком [StackOverflow](http://stackoverflow.com) или любой другой ссылкой, которая будет полезной, [отправьте нам сообщение электронной почты](mailto:aspnetue@microsoft.com?subject=Deployment%20Content%20Map) со ссылкой.
> 
> > [!NOTE] 
> > 
> > Многие из этих ресурсов описывают функции развертывания, доступные только при установке последнего выпуска [обновления веб-публикации Visual Studio](https://go.microsoft.com/fwlink/?LinkID=208120). Некоторые функции доступны только в Visual Studio 2012 или Visual Studio 2013.

Этот раздел состоит из следующих подразделов.

- [Общие сведения о вариантах развертывания для веб-проектов](#understanding)
- [Поиск поставщиков услуг размещения для приложения ASP.NET](#findinghosting)
- [Развертывание веб-приложения из Visual Studio](#fromvs)
- [Развертывание веб-приложения путем создания и установки пакета веб-развертывания](#package)
- [Развертывание веб-приложения с помощью процесса непрерывной интеграции (CI)](#ci)
- [Использование преобразований Web. config для изменения параметров в целевом файле Web. config или файле App. config во время развертывания](#transforms)
- [Использование параметров веб-развертывание для изменения параметров в целевом веб-приложении во время развертывания](#webdeployparms)
- [Проверка того, что приложение отключено во время развертывания](#appoffline)
- [Развертывание базы данных или внесение изменений в базу данных в процессе развертывания веб-приложения](#databasewithweb)
- [Развертывание базы данных отдельно от развертывания веб-приложения](#databaseseparate)
- [Развертывание веб-приложения, использующего службы приложений ASP.NET, такие как членство и профилирование](#aspnetmembership)
- [Предварительная компиляция для развертывания](#precompiling)
- [Развертывание веб-приложения интрасети](#intranet)
- [Автоматизация стандартных задач развертывания, которые не являются автоматическими](#automating)
- [Настройка веб-серверов для того, чтобы разработчики могли развертывать веб-приложения с помощью веб-развертывание](#configuringservers)
- [Настройка серверов для поставщика услуг размещения](#hostingprovider)
- [Устранение неполадок при развертывании](#troubleshooting)
- [Получение справки по определенному вопросу развертывания](#gettinghelp)
- [Дополнительные ресурсы](#additional)

<a id="understanding"></a>

## <a name="understanding-deployment-options-for-web-projects"></a>Общие сведения о вариантах развертывания для веб-проектов

- [Обзор веб-развертывания для Visual Studio и ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx) (MSDN).
- [Развертывание веб-сайта Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Описание параметров и ссылок на ресурсы для развертывания веб-проектов на веб-сайтах Windows Azure, включая [непрерывную доставку](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) (автоматизированное [Управление из системы управления версиями](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)), а также использование Visual Studio.
- [Усовершенствования веб-публикации в Visual Studio 2012](../visual-studio/overview/2012/visual-studio-2012-web-publishing-improvements.md) (видео Скотта Hanselman).
- [Обзор публикации для веб-развертывания в VS 2010](http://vishaljoshi.blogspot.com/2009/09/overview-post-for-web-deployment-in-vs.html) (блог Вишал Джоши). Старая запись блога, но некоторые ресурсы Visual Studio 2010, на которые он ссылается, содержат сведения, которые все еще актуальны для Visual Studio 2012.

<a id="findinghosting"></a>

## <a name="finding-hosting-providers-for-an-aspnet-application"></a>Поиск поставщиков услуг размещения для приложения ASP.NET

- [Размещение в ASP.NET](https://asp.net/hosting)

<a id="fromvs"></a>

## <a name="deploying-a-web-application-from-visual-studio"></a>Развертывание веб-приложения из Visual Studio

- [Развертывание веб-сайта Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Содержит описание параметров и ссылки на ресурсы для развертывания веб-проектов на веб-сайтах Windows Azure. Включает раздел о развертывании из Visual Studio.
- [Веб-развертывание ASP.NET с помощью Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). серия руководств, посвященных 12 компонентам, демонстрирует развертывание веб-приложений с помощью SQL Serverных баз данных. Для развертывания базы данных использует как поставщик Дбдакфкс, так и Entity Framework Code First Migrations. Также содержит сведения о [преобразованиях файлов Web. config](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md), [развертывании отдельных файлов](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md#specificfiles), [развертывании из командной строки](../web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment.md), а [также о настройке конвейера веб-публикаций Visual Studio путем редактирования файлов pubxml](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md). Применяется ко всем веб-проектам ASP.NET, включая веб-формы, MVC и веб-API.)
- [Инструкции. Развертывание веб-проекта с помощью публикации одним щелчком в Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) (справочные сведения о мастере веб-публикаций Visual Studio).
- [Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md). Это более ранняя версия **веб-развертывания ASP.NET с использованием Visual Studio** , указанной в верхней части этого раздела. В основном полезно в качестве сведений о развертывании баз данных SQL Server Compact и переходе с SQL Server Compact на полный выпуск SQL Server.
- [Многоуровневое приложение .NET, использующее таблицы хранилища, очереди и большие двоичные объекты](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure сайт). в серии руководств с 5 частями показано, как создать проект MVC и развернуть его в облачной службе Windows Azure.

<a id="package"></a>
## <a name="deploying-a-web-application-by-creating-and-installing-a-web-deployment-package"></a>Развертывание веб-приложения путем создания и установки пакета веб-развертывания

- [Как создать пакет веб-развертывания в Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx) (MSDN).
- [Инструкции по установке пакета развертывания с помощью файла deploy. cmd, созданного Visual Studio](https://msdn.microsoft.com/library/ff356104.aspx) (MSDN).
- [Использование пакета веб-развертывание для развертывания в службах IIS в окне разработчика и на узле стороннего производителя](http://sedodream.com/2011/11/08/UsingAWebDeployPackageToDeployToIISOnTheDevBoxAndToAThirdPartyHost.aspx) (блог Саид Хашими). Использование диспетчера IIS для установки пакета развертывания в службах IIS на локальном компьютере и в компании размещения, поддерживающей Диспетчер IIS для удаленного администрирования.
- [Создание пакета веб-развертывание из Visual Studio 2010](https://www.iis.net/learn/publish/using-web-deploy/building-a-web-deploy-package-from-visual-studio-2010) (веб-сайт IIS.NET). Содержит инструкции по созданию и установке пакетов командной строки.
- [Пакет публикуется в любом месте](http://sedodream.com/2012/03/14/PackageWebUpdatedAndVideoBelow.aspx) (блог Саид Хашими). Представляет пакет NuGet, который автоматизирует процесс преобразования файла Web. config для нескольких конечных сред, чтобы можно было развернуть один пакет на нескольких серверах. См. также [видео паккажевеб](https://www.youtube.com/watch?v=-LvUJFI8CzM) с помощью Саид Хашими.

См. также следующий раздел.

<a id="ci"></a>

## <a name="deploying-a-web-application-using-a-continuous-integration-ci-process"></a>Развертывание веб-приложения с помощью процесса непрерывной интеграции (CI)

- [Непрерывная интеграция и непрерывная поставка (создание облачных приложений в реальном мире с помощью Windows Azure).](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) Глава электронной книги, в которой представлены непрерывная интеграция и непрерывная поставка.
- [Развертывание веб-сайта Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Описывает параметры и ссылки на ресурсы для развертывания веб-проектов на веб-сайтах Windows Azure. Включает раздел об автоматизации развертывания из системы управления версиями.
- [Развертывание веб-приложений в корпоративных сценариях](../web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Руководство по 40. в этой статье показано, как автоматизировать развертывание в процессе непрерывной интеграции с помощью Visual Studio 2010 и Team Foundation Server 2010.
- В [Microsoft Build Engine: использование MSBuild и Team Foundation Build с помощью Саид Хашими и Уильям барсоломев](http://msbuildbook.com). Это книга, а не веб-ресурс, но она является основным руководством по настройке MSBuild для сценариев непрерывной интеграции.
- [Пакет расширения MSBuild](https://github.com/mikefourie/MSBuildExtensionPack). Включает задачи развертывания.
- [Инструкции по настройке сборки Team Foundation](https://aka.ms/vsarsolutions). Документация по параметрам управления жизненным циклом приложений в Team Foundation Server охватывает веб-развертывание и включает в себя учебники и видео.
- [Словчитах преобразования XML из CI-сервера](http://sedodream.com/2011/12/12/SlowCheetahXMLTransformsFromACIServer.aspx) (блог Саид Хашими). Объясняется, как использовать Словчитах, надстройку Visual Studio для преобразования файла App. config и других XML-файлов.

См. также проверка того, [что приложение находится в автономном состоянии во время развертывания](aspnet-web-deployment-content-map.md#appoffline) позже на этой странице.

<a id="transforms"></a>

## <a name="using-webconfig-transformations-to-change-settings-in-the-destination-webconfig-file-or-appconfig-file-during-deployment"></a>Использование преобразований Web. config для изменения параметров в целевом файле Web. config или файле App. config во время развертывания

- [Преобразования файла Web. config](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md).
- [Синтаксис преобразования Web. config для развертывания веб-проекта с помощью Visual Studio](https://msdn.microsoft.com/library/dd465326.aspx) (MSDN).
- [Веб-инструменты 2012,2 — преобразования Web. config](https://www.youtube.com/watch?v=HdPK8mxpKEI) (видео YouTube с Саид Хашими). Показывает, как настраивать и предварительно просматривать преобразования Web. config.
- [Разделы справки отключить преобразование web. config?](https://msdn.microsoft.com/library/ee942158.aspx#disable_web_config_transformation) (MSDN).
- [Когда следует использовать веб-развертывание параметры вместо преобразований Web. config?](https://msdn.microsoft.com/library/ee942158.aspx#web_deploy_parameters) (MSDN).
- [Xdt (преобразование XML-документов), выпущенное в CodePlex.com](https://blogs.msdn.com/b/webdev/archive/2013/04/23/xdt-xml-document-transform-released-on-codeplex-com.aspx) (блог веб-разработки и средств .NET). Объявляет о доступности исходного кода для модуля преобразования файла Web. config и выводит список средств, которые его используют.
- [Веб-сайты Windows Azure: как работают строки приложения и строки подключения](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure блоге). Альтернатива преобразованию Web. config, если конечная среда является веб-сайтами Windows Azure и требуется преобразовать `appSettings` или `connectionStrings`.

<a id="webdeployparms"></a>

## <a name="using-web-deploy-parameters-to-change-settings-in-the-destination-web-application-during-deployment"></a>Использование параметров веб-развертывание для изменения параметров в целевом веб-приложении во время развертывания

- [Как использовать веб-развертывание параметры в пакете веб-развертывания](https://msdn.microsoft.com/library/ff398068.aspx) (MSDN).
- [MSDeploy: как обновить параметры приложения при публикации на основе профиля публикации](http://sedodream.com/2013/03/02/MSDeployHowToUpdateAppSettingsOnPublishBasedOnThePublishProfile.aspx) (блог Саид Хашими). Показано, как интегрировать параметры веб-развертывания в профили публикации Visual Studio.
- [Веб-развертывание параметризации](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-parameterization) (веб-сайт IIS.NET).
- [Веб-развертывание параметризации в действии](http://vishaljoshi.blogspot.com/2010/07/web-deploy-parameterization-in-action.html) (блог Вишал Джоши).
- [Веб-развертываниее преобразование параметров и Web. config](http://vishaljoshi.blogspot.com/2010/06/parameterization-vs-webconfig.html) (блог Вишал Джоши).
- [Веб-сайты Windows Azure: как работают строки приложения и строки подключения](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure блоге). Альтернативой параметрам веб-развертывания, если конечная среда является веб-сайтами Windows Azure и необходимо параметризовать `appSettings` или `connectionStrings`.

<a id="appoffline"></a>

## <a name="making-sure-an-application-is-off-line-during-deployment"></a>Проверка того, что приложение отключено во время развертывания

- [ASP.NET веб-развертывание с помощью Visual Studio: развертывание обновления кода](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md). См. раздел **перевести приложение в автономный режим во время развертывания.**
- [Перевод приложения в автономный режим перед публикацией](https://www.iis.net/learn/publish/deploying-application-packages/taking-an-application-offline-before-publishing) (сайт IIS.NET). Описание встроенной функции веб-развертывание 3,0, которая автоматизирует обработку приложения\_автономном HTM-файле. Эта функция не работает с пользовательским приложением\_автономные HTM файлы.
- [Как перевести веб-приложение в автономный режим во время публикации](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx) (блог Саид Хашими). Автоматизация процесса использования пользовательского приложения\_автономного файла. htm.
- [Обновления веб-публикации для приложения в автономном режиме и усечекксум](https://blogs.msdn.com/b/webdev/archive/2013/10/30/web-publishing-updates-for-app-offline-and-usechecksum.aspx) (блог веб-разработки Майкрософт). Другой вариант автоматизации использования приложения\_автономного файла. htm.
- [Веб-развертывание 3,5 RTW](https://blogs.iis.net/msdeploy/archive/2013/07/09/webdeploy-3-5-rtw.aspx) (сайт IIS.NET). Новая функция веб-развертывание 3,5 для пользовательского приложения\_автономные HTM файлы.

<a id="databasewithweb"></a>

## <a name="deploying-a-database-or-changes-to-a-database-as-part-of-web-application-deployment"></a>Развертывание базы данных или внесение изменений в базу данных в процессе развертывания веб-приложения

- [Настройка развертывания базы данных в Visual Studio](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) (MSDN). Общие сведения о параметрах развертывания базы данных с помощью веб-проекта.
- [Веб-развертывание ASP.NET с помощью Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). серия руководств, посвященных 12 компонентам, демонстрирует развертывание базы данных с помощью поставщика Дбдакфкс и Entity Framework Code First Migrations.
- [Инструкции. Развертывание веб-проекта с помощью публикации одним щелчком в Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) (MSDN).
- [Развертывание безопасного приложения ASP.NET MVC 5 с членством, OAuth и базой данных SQL на веб-сайте Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Длинное руководство, которое создает и развертывает приложение, использующее одну базу данных SQL Server для членства и данных приложений.
- [Развертывание веб-приложения ASP.NET с SQL Server Compact с помощью Visual Studio](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md). серия руководств, посвященных 12 компонентам, демонстрирует развертывание баз данных SQL Server Compact и переход с SQL Server Compact на полный выпуск SQL Server.

См. также раздел Развертывание веб-приложения путем создания и установки пакета веб-развертывания и развертывания веб-приложения с помощью процесса непрерывной интеграции (CI), приведенного ранее на этой странице.

<a id="databaseseparate"></a>

## <a name="deploying-a-database-separately-from-web-application-deployment"></a>Развертывание базы данных отдельно от развертывания веб-приложения

- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx) (MSDN).
- [Включение данных в проект базы данных SQL Server](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx) (SQL Server Data Tools блоге группы). Развертывание схемы и данных при развертывании базы данных.
- [Развертывание базы данных в Windows Azure](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate) (Microsoft Azure сайте)
- [Миграция баз данных в базу данных SQL Windows Azure (ранее SQL Azure)](https://msdn.microsoft.com/library/windowsazure/ee730904.aspx) (MSDN).
- [Миграция базы данных на SQL Azure с помощью SSDT](https://blogs.msdn.com/b/ssdt/archive/2012/04/19/migrating-a-database-to-sql-azure-using-ssdt.aspx) (блог группы SQL Server Data Tools).
- [Перенос приложений, ориентированных на данные, в Windows Azure](https://msdn.microsoft.com/library/jj156154.aspx) (MSDN).
- [Миграция баз данных SQL Server в базу данных SQL Windows Azure](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).

<a id="aspnetmembership"></a>

## <a name="deploying-a-web-application-that-uses-aspnet-application-services-such-as-membership-and-profiling"></a>Развертывание веб-приложения, использующего службы приложений ASP.NET, такие как членство и профилирование

- [Развертывание безопасного приложения ASP.NET MVC 5 с членством, OAuth и базой данных SQL на веб-сайте Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Длинное руководство, которое создает и развертывает приложение, использующее одну базу данных SQL Server для членства и данных приложений.
- [ASP.NET Identity](https://asp.net/identity/). Ресурсы для ASP.NET Identity.
- [Веб-развертывание ASP.NET с помощью Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). в серии руководств из 12 частей показано, как развернуть базу данных членства ASP.NET.
- [Настройка веб-сайта, использующего службы приложений](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs.md). Для проектов веб-сайтов, но также подходит для проектов веб-приложений.
- [Пользователи и роли на рабочем веб-сайте](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs.md). Для проектов веб-сайтов, но также подходит для проектов веб-приложений.

<a id="precompiling"></a>

## <a name="precompiling-for-deployment"></a>Предварительная компиляция для развертывания

- [Обзор предварительной компиляции проекта веб-приложения ASP.NET](https://msdn.microsoft.com/library/aa983464.aspx) (MSDN).
- [Вкладка "Пакет/Публикация веб-сайта", свойства проекта](https://msdn.microsoft.com/library/dd410108.aspx) (MSDN).
- [Диалоговое окно "Дополнительные параметры предварительной компиляции"](https://msdn.microsoft.com/library/hh475319.aspx) (MSDN).

<a id="intranet"></a>

## <a name="deploying-an-intranet-web-application"></a>Развертывание веб-приложения интрасети

- [Используйте локальный вариант проверки подлинности в Организации (ADFS) с ASP.NET в Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/) (блог Витторио Берточчи.).
- [Создание сайта интрасети с помощью ASP.NET MVC](https://msdn.microsoft.com/library/gg703322(VS.98).aspx) (MSDN). Предыдущее пошаговое руководство записанный для Visual Studio 2010 не отражает существенных изменений в шаблонах проектов интрасети, появившихся в Visual Studio 2013.

<a id="automating"></a>

## <a name="automating-common-deployment-tasks-that-are-not-automated-out-of-the-box"></a>Автоматизация стандартных задач развертывания, которые не являются автоматическими

- [ASP.NET веб-развертывание с помощью Visual Studio: развертывание дополнительных файлов](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md).
- [Задание разрешений для папки в веб-публикации](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) (блог Саид Хашими).
- [Расширение файла целевых объектов для включения параметров реестра для пакета веб-проекта](https://blogs.msdn.com/webdevtools/archive/2010/02/09/how-to-extend-target-file-to-include-registry-settings-for-web-project-package.aspx) (блог по средствам веб-разработки).
- [Расширение преобразования XML (Web. config)](http://sedodream.com/2010/09/09/ExtendingXMLWebconfigConfigTransformation.aspx) (блог Саид Хашими). Показывает, как создавать пользовательские преобразования XDT.
- [Настраиваемый поставщик средства веб-развертывания (MSDeploy) принимает 1](http://sedodream.com/2010/03/11/WebDeploymentToolMSDeployCustomProviderTake1.aspx) (блог Саид Хашими). Показывает, как создать веб-развертывание настраиваемого поставщика.
- [Как упаковать и развернуть COM-компоненты](https://blogs.msdn.com/webdevtools/archive/2010/03/03/how-to-package-and-deploy-com-component.aspx) (блог по средствам веб-разработки).
- [Как упаковать сборки .NET](https://blogs.msdn.com/webdevtools/archive/2010/02/19/how-to-package-com-component.aspx) (блог по средствам веб-разработки). Развертывание сборок в GAC.
- [Создание скрипта. инициализируйте виртуальную машину Windows Azure для веб-сервера с IIS, веб-развертывание и другими компонентами](http://www.tugberkugurlu.com/archive/script-out-everything-initialize-your-windows-azure-vm-for-your-web-server-with-iis-web-deploy-and-other-stuff) (блог тугберк Угурлу).

<a id="configuringservers"></a>

## <a name="configuring-web-servers-so-that-developers-can-deploy-web-applications-to-them-using-web-deploy"></a>Настройка веб-серверов для того, чтобы разработчики могли развертывать веб-приложения с помощью веб-развертывание

- [Установка и настройка веб-развертывание для развертываний администратора и развертывания без прав администратора](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy) (сайт IIS.NET).

<a id="hostingprovider"></a>

## <a name="configuring-servers-for-a-hosting-provider"></a>Настройка серверов для поставщика услуг размещения

- [Microsoft ASP.NET 4 руководств по развертыванию](https://go.microsoft.com/fwlink/?LinkId=191365) (центр загрузки Майкрософт).
- [Создание XML-файла профиля](https://www.iis.net/learn/web-hosting/joining-the-web-hosting-gallery/generate-a-profile-xml-file) (IIS.NET site).

<a id="troubleshooting"></a>

## <a name="troubleshooting-deployment-problems"></a>Устранение неполадок при развертывании

- [Устранение неполадок веб-сайтов Windows Azure в Visual Studio](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) (Microsoft Azure сайте).
- [ASP.NET веб-развертывание с помощью Visual Studio: Устранение неполадок](../web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting.md).
- [Устранение распространенных проблем с веб-развертывание](https://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-common-problems-with-web-deploy).
- [Коды ошибок веб-развертывание](https://www.iis.net/learn/publish/troubleshooting-web-deploy/web-deploy-error-codes) (сайт IIS.NET).
- [Вопросы и ответы по веб-развертыванию для Visual Studio и ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx) (MSDN).
- [Основные различия между IIS и ASP.NET Development Server](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md).
- [Распространенные различия в конфигурации между разработкой и производством](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs.md).
- [Размещение ASP.NET приложений в среднем доверии](http://www.4guysfromrolla.com/articles/100307-1.aspx) (4 из ролла сайта).

<a id="gettinghelp"></a>

## <a name="getting-help-with-a-specific-deployment-question"></a>Получение справки по определенному вопросу развертывания

- [Форум по настройке и развертыванию ASP.NET](https://forums.asp.net/26.aspx/1?Configuration and Deployment).
- [StackOverflow.com](http://www.StackOverflow.com).

<a id="additional"></a>

## <a name="additional-resources"></a>Дополнительные ресурсы

В этом разделе приводятся ссылки на дополнительные ресурсы, которые полезны для изучения того, как использовать средства развертывания Visual Studio и служб IIS.

В следующих блогах часто содержатся сведения о веб-развертывании Visual Studio:

- [Веб-средства разработки в блоге Майкрософт](https://blogs.msdn.com/b/webdevtools/).
- [Блог Саид Хашими](http://www.sedodream.com/).

Следующие ресурсы содержат документацию по веб-развертывание, платформе IIS, которую Visual Studio использует для выполнения задач развертывания проекта веб-приложения. Вы можете задать вопросы о веб-развертывание на [форуме средства веб-развертывания](https://go.microsoft.com/fwlink/?LinkId=149411) на веб-сайте IIS.NET.

- [Введение в веб-развертывание](https://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy).
- [Установка и настройка веб-развертывание](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy).
- [Скрипты PowerShell для автоматизации установки веб-развертывание](https://www.iis.net/learn/publish/using-web-deploy/powershell-scripts-for-automating-web-deploy-setup).
- [Средство веб-развертывания](https://go.microsoft.com/fwlink/?LinkId=151481). Узел оглавления верхнего уровня для веб-развертывание документации на сайте TechNet. Содержит полезные справочные сведения, но большинство страниц TechNet не обновлялись в течение нескольких лет.
- [Пространство имен Microsoft. Web. Deployment](https://go.microsoft.com/fwlink/?LinkId=148630). Документация по API не была обновлена после версии 1,0.
- [Блог группы веб-развертывания Майкрософт](https://blogs.iis.net/msdeploy/default.aspx).
- [Вкладка "публикация" на веб-сайте IIS.NET](https://www.iis.net/learn/publish).
