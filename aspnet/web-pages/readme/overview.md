---
uid: web-pages/readme/overview
title: Файл readme для WebMatrix | Документация Майкрософт
author: rick-anderson
description: Файл сведений о выпуске WebMatrix и веб-страницы ASP.NET (Razor) 1,0
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454272"
---
# <a name="webmatrix-readme"></a>Файл сведений для WebMatrix

13 января 2011

## <a name="contents"></a>Содержимое

> [!NOTE]
> Этот файл readme относится к выпуску 1,0 WebMatrix.

- [Обзор](#Overview)
- [Установка](#Installation_Notes)
- [Публикация приложений](#InstructionsForPublishingApplications)
- [Изменения и проблемы](#ChangesAndIssues)

    - [Установка WebMatrix 1,0](#Known_Issues_Installation)
    - [Веб-страницы ASP.NET](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [Установка приложений](#Known_Issues_Installing_Applications)
    - [Публикация приложений](#Known_Issues_Publishing_Applications)
- [Дополнительные сведения](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>Обзор

> Microsoft WebMatrix 1,0 — это бесплатный стек веб-разработки, устанавливаемый за считанные минуты. Он интегрирует веб-сервер с платформами баз данных и программирования для создания единого интегрированного интерфейса. WebMatrix можно использовать для оптимизации кода, тестирования и публикации собственного веб-сайта ASP.NET или PHP. также можно использовать WebMatrix для запуска нового веб-сайта с помощью популярных приложений с открытым исходным кодом, таких как DotNetNuke, Umbraco, WordPress или Joomla. WebMatrix использует тот же мощный веб-сервер, ядро СУБД и среду, которая будет запускать ваш веб-сайт в Интернете, что делает переход от разработки к рабочей среде беспрепятственно и плавно.

<a id="Installation_Notes"></a>

## <a name="installation"></a>Установка

> Чтобы установить WebMatrix 1,0, необходимо сначала установить [установщик веб-платформы Майкрософт 3,0](https://go.microsoft.com/fwlink/?LinkID=194638). После установки установщика веб-платформы его можно использовать для установки WebMatrix.
> 
> При возникновении проблем во время установки обратитесь к разделу [Устранение неполадок с установщик веб-платформы Майкрософт](https://go.microsoft.com/fwlink/?LinkId=196212).

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>Публикация приложений

> См. [Пошаговые инструкции по публикации приложений](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>Изменения и проблемы

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>Проблемы с установкой WebMatrix 1,0

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>Вопрос. WebMatrix 1,0 доступен только на платформах, поддерживающих Microsoft .NET Framework 4.

> Для WebMatrix требуется .NET Framework версии 4. В некоторых случаях установщик WebMatrix 1,0 попытается установить на платформу, которая не входит в набор поддерживаемых конфигураций. В частности, Windows Vista без обновления с пакетом обновления 1 (SP1) позволит начать установку WebMatrix, но компонент .NET Framework 4 завершится сбоем и заблокирует установку.
> 
> **Обходное решение**  
> Установите на поддерживаемой платформе, которая включает в себя:
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista с пакетом обновления 1 (SP1) или выше
> - Windows XP с пакетом обновления 3 (SP3)
> - Windows Server 2003 с пакетом обновления 2 (SP2)

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>Ошибка: не удается установить WebMatrix 1,0, если Microsoft Visual Studio 2008 установлен без Microsoft Visual Studio 2008 с пакетом обновления 1 (SP1)

> **Обходное решение**  
> Установите [Microsoft Visual Studio 2008 с пакетом обновления 1 (SP1)](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) из центра загрузки Майкрософт.

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>Причина. Некоторые сборки для SQL Server Compact 4,0 не установлены в GAC

> Управляемые сборки для SQL Server Compact 4,0 не помещаются в глобальный кэш сборок (GAC) при установке SQL Server Compact 4,0 на 64-разрядном компьютере, а на компьютере установлен только клиентский профиль .NET Framework 3,5 SP1. В глобальный кэш сборок не установлены следующие управляемые сборки:
> 
> - *System. Data. SqlServerCe. dll* (поставщик ADO.NET)
> - *System. Data. SqlServerCe. Entity. dll* (ADO.NET Entity Framework)
> 
> **Обходное решение**  
> Удалите SQL Server Compact 4,0. Скачайте и установите полную версию .NET Framework 3,5 с пакетом обновления 1 (SP1) из следующего расположения:  
>   
> [Microsoft .NET Framework 3,5 с пакетом обновления 1 (SP1) (полный пакет)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> Затем переустановите SQL Server Compact 4,0.

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>Ошибка: не удается удалить SQL Server Compact с помощью командной строки

> Удаление SQL Server Compact с помощью параметров командной строки не работает в этом выпуске.
> 
> **Обходное решение**  
> Используйте *программы и компоненты* на панели управления Windows для удаления Microsoft SQL Server Compact 4,0.

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>Веб-страницы ASP.NET

В этом разделе документа описаны новые функции, изменения и известные проблемы с выпуском 1,0 веб-страницы ASP.NET с синтаксис Razor.

- [Новые функции](#NewFeatures)
- [Изменения](#Changes)
- [Проблемы](#Issues)

#### <a id="NewFeatures"></a>Новые возможности

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>Новый: добавлен параметр конфигурации для отключения диспетчера пакетов

> Новый ключ `asp:AdminManagerEnabled` доступен для элемента `<appSettings>` в файле *Web. config* , который позволяет полностью отключить диспетчер пакетов. Значение по умолчанию для этого элемента равно true, то есть если оно не включено в файл *Web. config* , диспетчер пакетов включен. Чтобы отключить диспетчер пакетов, добавьте следующий элемент в файл *Web. config* в корневой папке веб-сайта:
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>Изменениями

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>Изменение: раздел "веб-страницы: Админфолдервиртуалпас" переименован в "ASP: Админфолдервиртуалпас"

> Ключ `webPages:AdminFolderVirtualPath`, который можно добавить в файл *Web. config* для указания расположения диспетчера пакетов, был переименован для использования пространства имен `asp:` вместо пространства имен `webPages`. Если вы использовали этот элемент, необходимо переименовать его в файле конфигурации.

#### <a id="Issues"></a> Известные проблемы

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>Ошибка: пароли для пользователей членства больше не распознаются

> Алгоритм создания и сохранения паролей членства (имени входа) был изменен для обеспечения большей безопасности. В результате пароли, сохраненные для участников (пользователей), созданных в бета-версиях ASP.NET Razor, не будут распознаны. 
> 
> **Обходной путь** Если сайт еще не помещен в рабочую среду, удалите записи пользователей из базы данных членства. Если база данных находится в режиме реального времени, программным способом повторное создание существующих паролей в базе данных членства.

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>Причина: непредвиденное поведение при использовании пользовательской таблицы пользователя для членства

> Чтобы инициализировать поставщик членства для веб-сайта ASP.NET Razor, вызовите метод `WebSecurity.InitializeDatabaseConnection`. (В WebMatrix шаблон начального сайта включает вызов этого метода в файле *\_AppStart. cshtml* .) Если для параметра `autoCreateTables` этого метода задано значение true (по умолчанию задано значение true в шаблоне начального сайта) и если в метод передается нераспознанное имя таблицы (второй параметр), метод не вызывает ошибку. Вместо этого он автоматически создает таблицу.
> 
> Это может быть проблемой, если вы планируете использовать настраиваемую таблицу пользователей для членства, но передать неправильное имя таблицы в метод `WebSecurity.InitializeDatabaseConnection`. Так как метод не по умолчанию вызывает ошибку, если указанная таблица не существует, и, поскольку вместо этого создается новая таблица, приложение может работать нормально. Однако код приложения, основанный на настраиваемой пользовательской таблице (и в полях), может в конечном итоге завершиться с непредвиденными ошибками.
> 
> **Обходное решение**  
> Убедитесь, что имя, переданное в методе `InitializeDatabaseConnection`, совпадает с таблицей профиля пользователя в базе данных членства или убедитесь, что для параметра `autoCreateTables` задано значение false.

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a>Ошибка: сообщение об ошибке "модулю администрирования требуется доступ к ~/АПП\_Data"

> В некоторых обстоятельствах попытка создать пользователей или иным образом работать с системой членства в ASP.NET может привести к тому, что на странице будет отображаться сообщение об ошибке " *для модуля администрирования требуется доступ к ~/апп\_Data*. Это происходит, если учетная запись, от которой выполняется IIS или IIS Express, не имеет разрешений на создание и запись в папку *данных приложения\_* в корневом каталоге веб-сайта. 
> 
> **Обходной путь** Вручную создайте папку *данных\_приложений* для веб-сайта. Затем убедитесь, что учетная запись Windows, под которой выполняется приложение (обычно СЕТЕВая служба), имеет разрешения на чтение и запись для корневых папок приложения и для вложенных папок, таких как данные приложения\_. Более подробные сведения см. в статье базы знаний [проблемы с SQL Server Express проектами создания пользовательских экземпляров и ASP.NET проектов веб-приложений](https://support.microsoft.com/kb/2002980).

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>Ошибка: "не удалось создать пользовательский экземпляр SQL Server"

> Если веб-приложение WebMatrix использует SQL Server Express и работает с IIS 7,5 в Windows 7 или Windows Server 2008 R2, может появиться сообщение об ошибке, свидетельствующее о том, что SQL Server не может получить путь к локальному приложению пользователя во время выполнения.
> 
> **Обходной путь** Убедитесь, что учетная запись Windows, под которой выполняется приложение (обычно СЕТЕВая служба), имеет разрешения на чтение и запись для корневых папок приложения и для вложенных папок, таких как *данные\_приложений*. Более подробные сведения см. в статье базы знаний [проблемы с SQL Server Express проектами создания пользовательских экземпляров и ASP.NET проектов веб-приложений](https://support.microsoft.com/kb/2002980).

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>Вопрос. файлы, содержащие ресурсы диспетчера пакетов или пароли диспетчера пакетов, обслуживаемые в IIS 6,0 и более ранних версиях

> Если вы развертываете приложение веб-страницы ASP.NET (Razor), которое было создано с помощью выпуска RC2, и если приложение содержит файл *Password. txt* или *паккажесаурцес. txt* в */АПП\_Data/Admin*, IIS 6,0 будет обслуживать файл по запросу, потенциально предоставляя пароли для экземпляра диспетчера пакетов. 
> 
> **Обходной путь** Переименование файла *Password. txt* или *паккажесаурцес. txt* в файл *Password. config* или *паккажесаурцес. config*. По умолчанию службы IIS 6,0 не обслуживает файлы с расширением *config* . (В IIS 7 файлы в папке *приложения\_данных* не обслуживаются, поэтому переименовывать файлы не нужно).

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>Причина. при удалении пакетов, установленных с помощью бета-версии 3, компоненты пакета не полностью удаляются.

> Если пакет был установлен с помощью диспетчера пакетов в выпуске Beta 3, а затем попытаться удалить его с помощью текущего выпуска, пакет не будет полностью удален. С помощью кнопки **удаления** диспетчера пакетов можно удалить некоторые компоненты, но оставить код библиотеки пакета и не обновить файл *Package. config* .
> 
> **Обходной путь**   
> Выполните следующие действия.  
> 1. Удалите папку *приложения\_дата\паккажес* . При этом удаляются все пакеты.   
> 2. Удалите файл *Packages. config* в корневой папке веб-сайта.

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>Вопрос. в Visual Studio при вызове диспетчера пакетов на основе веб-приложений приложение переводится в автономный режим.

> Если вы работаете в Visual Studio (не в WebMatrix) и используете *\_функцию администрирования* для запуска диспетчера пакетов, Visual Studio переводит приложение в автономный режим и отправляет приложение *\_offline. htm* в корневую папку веб-сайта, что нарушает возможность использования диспетчера пакетов.
> 
> [!NOTE]
> Хотя это поведение обычно встречается при использовании веб-интерфейса диспетчера пакетов, такое же поведение возникает при добавлении, удалении или изменении любых файлов в папке *приложения\_данных* .
> 
> **Обходной путь**   
> Для работы с пакетами в Visual Studio используйте расширение NuGet вместо диспетчера пакетов на основе веб-служб. Дополнительные сведения см. в [документации по NuGet](https://docs.microsoft.com/nuget/). Если вы работаете с другими файлами в папке *приложения\_данных* , рекомендуется хранить их в другом расположении, чтобы избежать этой проблемы. Если это непрактично, удалите *приложение\_автономный htm* -файл вручную или дождитесь, пока сайт снова не вернется в оперативный режим (по умолчанию через 30 секунд).

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>Вопрос. шаблоны IntelliSense и проектов Visual Studio доступны только в ASP.NET MVC версии 3

> При установке веб-страницы ASP.NET также не устанавливаются средства для Visual Studio, такие как IntelliSense и шаблоны проектов для веб-страницы ASP.NET приложений.
> 
> **Обходной путь** Чтобы использовать IntelliSense и шаблоны проектов для веб-страницы ASP.NET приложений в Visual Studio, установите ASP.NET MVC 3 RC либо через установщик веб-платформы, либо в [автономный установщик](https://go.microsoft.com/fwlink/?LinkID=191797).

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>Ошибка: чтение веб-каналов или других внешних данных через прокси Server

> Если сервер, на котором работает сайт, находится за прокси-сервером, может потребоваться настроить сведения о прокси-сервере в файле *Web. config* , чтобы иметь возможность считывать сведения, поступающие за пределы сайта. Например, при использовании вспомогательного метода `ReCaptcha` вспомогательный объект взаимодействует со службой reCAPTCHA, но может быть заблокирован прокси-сервером. Аналогичным образом, для веб-каналов, используемых в веб-страницы ASP.NET, например в канале, используемом диспетчером пакетов, может потребоваться настройка прокси.
> 
> Если возникают проблемы при работе с внешней службой или веб-каналом пакета, добавьте следующие элементы в корневой файл *Web. config* приложения:
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> Дополнительные сведения о настройке прокси-сервера см. в разделе [&lt;прокси-&gt; элемент (параметры сети)](https://msdn.microsoft.com/library/sa91de1e.aspx) на веб-сайте MSDN.

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>Ошибка: при удалении .NET Framework версии 4 отключается веб-страницы ASP.NET с синтаксисом Razor.

> Если удалить .NET Framework версии 4, а затем переустановить ее, веб-страницы ASP.NET с синтаксис Razor будет отключена. Страницы с расширением *CSHTML* выполняются неправильно. Веб-страницы ASP.NET регистрирует сборку в корневом файле *Web. config* компьютера, а удаление .NET Framework удаляет этот файл. При переустановке .NET Framework устанавливается новая версия файла конфигурации, но не добавляется ссылка на сборку веб-страницы ASP.NET.
> 
> **Обходной путь** После переустановки .NET Framework переустановите веб-страницы ASP.NET с синтаксис Razor. В файл *Web. config* в корневой папке компьютера будет добавлен следующий элемент, который обычно находится в следующем расположении:  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>Ошибка: URL-адреса без расширений не могут найти файлы. cshtml/. vbhtml в IIS 7 или IIS 7,5

> В IIS 7 или IIS 7,5 запросы с URL-адресом, следующим как, не могут найти страницы с расширением *CSHTML* или *VBHTML* :  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> Эта ошибка возникает, поскольку переписывание URL-адресов не включено по умолчанию для IIS 7 или IIS 7,5. Сценарий ликелиест заключается в том, что вы не видите проблему при локальном тестировании с помощью IIS Express, но при развертывании веб-сайта на веб-сайте размещения эта проблема возникает.
> 
> **Обходное решение**
> 
> - При наличии контроля над компьютером сервера установите обновление, описанное в разделе [обновление, которое позволяет определенным обработчикам iis 7,0 или iis 7,5 выполнять запросы, URL-адреса которых не заканчиваются точкой](https://support.microsoft.com/kb/980368).
> - Если у вас нет контроля над компьютером сервера (например, при развертывании на веб-сайте размещения), добавьте следующий адрес в файл *Web. config* веб-сайта: 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>Вопрос. Развертывание приложения на компьютере, на котором не установлен SQL Server Compact

> Приложения, включающие SQL Server Compact базы данных, могут выполняться на компьютере, где не установлена SQL Server Compact. Microsoft WebMatrix 1,0 автоматически копирует эти двоичные файлы и выполняет соответствующие преобразования файла *Web. config* .
> 
> **Обходной путь** Если необходимо скопировать эти файлы и внести изменения в файл *Web. config* вручную, выполните следующие действия.
> 
> 1. Скопируйте сборки ядра СУБД в папку *bin* (и вложенные папки) приложения на целевом компьютере:  
> 
>    - Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*   
>      **в** *\bin*
>    - Копирование *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **в** *\Bin\x86*
>    - Копирование *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * **в** *\Bin\amd64*
> 
> 2. В корневой папке веб-сайта создайте или откройте файл *Web. config* . (В WebMatrix 1,0 этот тип файлов доступен, если в диалоговом окне **Выбор типа файла** щелкнуть **все** .)
> 3. Добавьте следующий элемент в качестве дочернего для элемента `<configuration>` (не внутри элемента `<system.web>`):
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>Ошибка: вспомогательные функции "база данных" и "Сетка" не работают со средним уровнем доверия в Visual Basic

> Если вы используете Visual Basic (создание файлов *. vbhtml* ), вспомогательные средства `Database` и `WebGrid` не будут работать, если приложение настроено для использования среднего уровня доверия.
> 
> **Обходное решение**  
> Если вы используете Visual Studio 2010, эту проблему можно устранить, установив выпуск с пакетом обновления 1 (SP1). Пока не будет доступна окончательная версия пакета обновления 1 (SP1), вы можете загрузить бета-версию пакета обновления 1 (SP1) с веб-страницы [Microsoft Visual Studio 2010 с пакетом обновления](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) SP1 в центре загрузки Майкрософт.   
>   
> Если это непрактично или если вы не используете Visual Studio 2010, можно временно настроить приложение для использования полного доверия.

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>Причина: ресурсы "Аппликатионпарт" доступны извне.

> Если сборка содержит объекты, производные от класса `ApplicationPart`, то ресурсы этой сборки предоставляются классом `ResourceRouteHandler`. Например, рассмотрим следующий URL-адрес:  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> Этот запрос скачивает все строки ресурсов в сборке *System. Web. веб-страниц. Administration. dll* . Скачаны все внедренные ресурсы (даже те, которые не предназначены для обслуживания в виде статического содержимого). Если внедренные ресурсы содержат конфиденциальные сведения, это может представлять угрозу безопасности. 
> 
> **Обходной путь**   
> При создании объекта **аппликатионпарт** убедитесь, что внедренные ресурсы, связанные с этой сборкой объекта **аппликатионпарт** , не содержат конфиденциальную информацию.

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> Сведения о проблемах установки для WebMatrix см. в разделе [проблемы установки WebMatrix](#Known_Issues_Installation) ранее в этом документе.

В этом разделе документа описаны известные проблемы среды разработки WebMatrix.

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>Ошибка. изменения имени пользователя или пароля строки подключения к базе данных в файле Web. config не отражаются в рабочей области базы данных.

> **Обходное решение**  
> 
> 1. В файле *Web. config* измените имя базы данных в строке подключения (например, добавьте в нее "1").
> 2. Сохраните файл *Web. config* .
> 3. Щелкните **базы данных** и обновить.
> 4. Измените имя базы данных в строке подключения в файле *Web. config* на исходное имя базы данных.
> 5. Сохраните файл *Web. config* .
> 6. Щелкните **базы данных** и обновить.

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>Ошибка: невозможно удалить папки, созданные WebMatrix

> Если WebMatrix работает с повышенными разрешениями (то есть запущен WebMatrix с помощью команды **Запуск от имени администратора** в Windows), папки, созданные WebMatrix, нельзя удалить с помощью проводника Windows.
> 
> **Обходное решение**  
> Запустите проводник Windows с повышенными разрешениями. Выполните следующие действия.  
> 
> 1. В Windows нажмите кнопку **Пуск**.
> 2. Введите "Проводник Windows" и щелкните правой кнопкой мыши запись **проводника Windows**.
> 3. Щелкните **Запуск от имени администратора**. Затем можно удалить папки.

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>Ошибка: WebMatrix 1,0 не может выполнить определенные задачи, требующие повышения прав

> WebMatrix 1,0 не может выполнять определенные задачи, требующие повышения прав, например установку дополнительных компонентов в следующих ситуациях:
> 
> - В Windows Vista или Windows 7 вы выполнили вход с учетной записью, не обладающей правами администратора, и отключена функция контроля учетных записей (UAC).
> - Вы используете Microsoft Windows XP или Microsoft Windows Server 2003.
> 
> **Обходное решение**  
> Для большинства задач в WebMatrix 1,0 не требуются административные разрешения. Для тех, кто может выполнить операцию от имени администратора, или выполните следующие действия.
> 
> - В Windows Vista или Windows 7 включите UAC.
> - В Windows XP добавьте пользователя в группу безопасности Администраторы.

#### <a name="issue-site-from-web-gallery-is-disabled"></a>Ошибка: "сайт из веб-коллекции" отключен

> Параметр **сайт из веб-коллекции** отключен, если установщик веб-платформы 3,0 не установлен.
> 
> **Обходное решение**  
> Установите [установщик веб-платформы Майкрософт 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>Причина: Google Chrome недоступен в качестве варианта выполнения

> Google Chrome не отображается в списке браузеров в разделе **Запуск** на вкладке **Главная** .
> 
> **Обходное решение**  
> Некоторые версии Google Chrome неправильно регистрируются в компоненте "программы по умолчанию" в Windows. В качестве обходного решения запустите Google Chrome, щелкните меню *Настройка и управление Google Chrome* , щелкните *Параметры*, а затем выберите команду *сделать Google Chrome браузером по умолчанию*.

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>Проблема. диалоговое окно "внешний ключ" не позволяет ввести первичный ключ

> Диалоговое окно **внешний ключ** не позволяет ввести имя первичного ключа из таблицы первичного ключа.
> 
> **Обходное решение**  
> Это сделано намеренно. Не нужно вводить имя первичного ключа из таблицы первичного ключа.

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>Ошибка. Технология IntelliSense недоступна в WebMatrix для синтаксис Razor C#, или Visual Basic

> Технология IntelliSense поддерживается в WebMatrix для HTML и CSS. Однако он недоступен для других языков. 
> 
> **Обходной путь**   
> Нет.

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>Вопрос. IntelliSense для HTML и CSS предлагает элементы, которые не соответствуют контексту.

> Технология IntelliSense для разметки в WebMatrix поддерживает HTML, используя [переходную схему XHTML 1,0](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) и CSS с помощью [схемы CSS 2,1](http://www.w3.org/TR/CSS2/). Поскольку технология IntelliSense основана на этих конкретных схемах, могут быть предложены некоторые теги, атрибуты или свойства, которые не подходят для текущей страницы или определения стиля. Для HTML это также может привести к непредвиденным рекомендациям в содержимом, которое может интерпретироваться как неправильно сформированное XHTML (например, если теги не закрыты). Эта проблема может быть более заметной, если точка вставки находится внутри неполного тега. в этом случае IntelliSense может предложить новые открывающие теги или предложить другие неправильные рекомендации. 
> 
> **Обходной путь**   
> Для HTML убедитесь, что вы работаете на правильно сформированной, полной странице XHTML. Для CSS нет решения.

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>Причина: технология IntelliSense не вызывается при вводе

> В некоторых случаях IntelliSense может не вызываться, так как в редакторе не введен HTML или CSS. В частности, это может произойти, когда точка вставки расположена непосредственно рядом с другим элементом или в конце файла. 
> 
> **Обходной путь**   
> Убедитесь, что вокруг точки вставки имеется пробел, а точка вставки не находится в конце файла. Можно также вызвать IntelliSense вручную, нажав клавиши Ctrl + пробел.

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>Ошибка: Пользовательский интерфейс для отключения IntelliSense недоступен

> WebMatrix 1,0 не предоставляет пользовательского интерфейса или жеста для отключения IntelliSense. 
> 
> **Обходной путь**   
> Запустите WebMatrix с помощью следующей команды, которая включает параметр, который отключает IntelliSense:  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express.

IIS Express имеет собственный файл сведений, доступный по следующему URL-адресу:

[https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x409](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact имеет собственный файл сведений, доступный по следующему URL-адресу:

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

Сведения о проблемах, связанных с установкой SQL Server Compact в составе WebMatrix, см. в разделе [проблемы установки WebMatrix](#Known_Issues_Installation) ранее в этом документе.

### <a id="Known_Issues_Installing_Applications"></a>Установка приложений

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>Причина. Установка приложения может занять много времени, если папка пользователя "Мои документы" перенаправлена в общую сетевую папку

> **Обходное решение**  
> Нет. Установка приложения может занять некоторое время, но будет установлена правильно.

### <a id="Known_Issues_Publishing_Applications"></a>Публикация приложений

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>Ошибка: при публикации базы данных SQL Compact появляется сообщение об ошибке "не удается получить необходимые разрешения"

> WebMatrix не полностью поддерживает развертывание вспомогательных двоичных файлов для SQL Server Compact на сервере под управлением .NET Framework версии 3,5 с конфигурацией среднего уровня доверия.
> 
> **Обходное решение**  
> Наиболее предпочтительным решением является установка .NET Framework 4 на сервере. Кроме того, выполните следующие действия.
> 
> 1. Добавьте следующие элементы в раздел `SecurityClasses` в файле *Web\_медиумтруст. config* :
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. Создайте новый набор разрешений в файле *Web\_медиумтруст. config* со следующими необходимыми разрешениями:
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. Примените набор разрешений к SQL Server Compact, поместив следующие элементы в файл *Web\_медиумтруст. config* :
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>Причина: в коллекции и веб-приложениях PhpBB отображается ошибка "Служба недоступна" после публикации

> В некоторых случаях публикация приложения приводит к ошибке "Служба недоступна".
> 
> **Обходное решение**  
> В WebMatrix добавьте обратную косую черту (\) в конец имени сервера в окне **Параметры публикации** , а затем опубликуйте приложение еще раз.

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>Причина: макет веб-сайта Moodle и ссылки не нарушаются после публикации

> После публикации приложения Moodle приложение работает неправильно.
> 
> **Обходное решение**  
> В WebMatrix добавьте косую черту (/) в конец поля **имя сайта** в окне **Параметры публикации** , а затем опубликуйте приложение еще раз.

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>Ошибка: сбой публикации nopCommerce с ошибкой базы данных

> Публикация nopCommerce завершается сбоем и сообщает об ошибке базы данных, например "Ошибка вставки в таблицу журнала\_NOP".
> 
> **Обходное решение**  
> 
> 1. В WebMatrix щелкните **запустить** , чтобы запустить nopCommerce локально.
> 2. Войдите на страницу администрирования.
> 3. Щелкните **системное** меню.
> 4. Выберите параметр **Журнал** .
> 5. Нажмите кнопку **Очистить журнал**.
> 6. Опубликуйте nopCommerce еще раз.

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>Ошибка. при скачивании опубликованного сайта в Силверстрипе CMS отображается сообщение об ошибке HTTP 500 PHP FCGI.

> **Обходное решение**  
> После нажатия кнопки **скачать опубликованный сайт**пропустите `silverstripe-cache/manifest_main` в **предварительной версии публикации**. Этот файл используется в целях кэширования и зависит от конкретного компьютера.

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>Ошибка: при скачивании опубликованного сайта в подтексте отображается сообщение об ошибке сервера в "/" приложении ".

> **Обходное решение**  
> Откройте файл *Web. config* сайта и замените идентификатор пользователя и пароль в строке подключения к базе данных учетными данными администратора SQL Server (учетные данные SA).
> 
> Кроме того, чтобы предоставить учетной записи пользователя, к которой вы выполнили вход, разрешения `db_owner`, выполните следующие действия:
> 
> 1. Установите SQL Server Management Studio с помощью установщика веб-платформы.
> 2. Подключитесь к локальному экземпляру SQL Server Express (по умолчанию `.\SQLEXPRESS`).
> 3. Щелкните **базы данных** &gt; *[Локалсубтекстдатабасе]* &gt; **Безопасность** &gt; **Пользователи** &gt; *[локалсубтекстусер*] (по умолчанию — `subtextuser`], щелкните правой кнопкой мыши и выберите пункт **Свойства**.
> 4. Выберите **база данных\_владелец** в разделе членство в роли.

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>Проблема. После публикации сайт может не работать, если поле "URL-адрес назначения" не имеет префикса http://или https://

> Если в диалоговом окне **Параметры публикации** URL-адрес назначения не начинается с `http://` или `https://`, сайт может не работать после развертывания.
> 
> **Обходное решение**  
> Убедитесь, что перед публикацией сайта URL-адрес назначения в диалоговом окне " **Параметры публикации** " начинается с `http://` или `https://`.

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>Ошибка. Публикация базы данных MySQL завершается сбоем с ошибкой "не удалось опубликовать базу данных. Это может произойти, если удаленная база данных не может выполнить скрипт ".

> Эта ошибка может возникать по ряду причин. Одной из причин возникновения этой ошибки является то, что скрипт базы данных содержит символ одинарной кавычки ('), а кодировка по умолчанию целевой базы данных MySQL — не UTF-8.
> 
> **Обходное решение**  
> Задайте в качестве кодировки по умолчанию для удаленной базы данных MySQL кодировку UTF-8.

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>Причина. Некоторые ссылки не отображаются в DotNetNuke после публикации или скачивания сайта

> Если вы публикуете или скачиваете сайт DotNetNuke, может потребоваться очистить кэш, чтобы отобразить новые ссылки на сайте.
> 
> **Обходное решение**
> 
> 1. Войдите в систему как "узел".
> 2. Перейдите в меню узел и выберите **Параметры узла**.
> 3. Прокрутите вниз и в разделе **Дополнительные параметры**разверните узел **Параметры производительности**.
> 4. Щелкните ссылку **очистить кэш** для страниц.
> 5. Перейдите в нижнюю часть страницы и перезапустите приложение.

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>Причина. при скачивании опубликованного сайта некоторые ссылки в Атомсите нарушаются

> **Обходное решение**  
> В файле *Service. config* , файле *Users. config* и всех *XML-* файлах замените строку URL-адреса (например, `http://myhost.com/atomsite`) на локальную (например, `http://localhost:1239`).

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>Ошибка: приложениям на основе MySQL, например WordPress, не удалось опубликовать и сообщить об ошибке базы данных

> По умолчанию WebMatrix устанавливает MySQL с кодировкой UTF-8. Если вы устанавливаете MySQL самостоятельно, а кодировка не UTF-8 (например, это Latin1), процесс публикации баз данных может завершиться ошибкой.
> 
> **Обходное решение**
> 
> 1. Измените кодировку MySQL на UTF-8. (Дополнительные сведения см. в разделе [Серверный набор символов и параметры сортировки](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) на веб-сайте MySQL.)
> 2. Переустановите приложение.
> 3. Повторно опубликуйте приложение.

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>Ошибка: "скачивание опубликованного сайта" завершается неудачей для приложений, имеющих браузерную установку

> Для некоторых приложений (например, Kentico CMS) требуется запустить их в браузере, чтобы выполнить установку после установки, например создать базу данных. Если вы публикуете приложение подобным образом, не выполняя настройку на основе браузера, попытка скачать тот же сайт с удаленного сервера завершится ошибкой.
> 
> **Обходное решение**  
> Завершите настройку на основе браузера перед публикацией сайта.

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>Ошибка: "скачивание опубликованного сайта" завершается сбоем с ошибкой базы данных для DotNetNuke и Kooboo CMS.

> При попытке загрузить приложение с сервера и наличии учетных данных администратора в строке подключения к базе данных в диалоговом окне " **Параметры публикации** " в журнале публикации может появиться следующее сообщение об ошибке:
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **Обходное решение**  
> Если это целесообразно, повторно опубликуйте сайт (или разработайте его), используя учетные данные без прав администратора для базы данных.

<a id="More_Info"></a>

## <a name="for-more-information"></a>Дополнительные сведения см. в разделе

Дополнительные сведения о WebMatrix 1,0 см. на следующих веб-сайтах:

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© Корпорация Майкрософт (Microsoft Corporation), 2011. Все права защищены. [Условия использования](https://msdn.microsoft.cos/cc300389.aspx).
