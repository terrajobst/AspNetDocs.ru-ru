---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs
title: Распространенные различия в конфигурации между разработкой и производством (C#) | Документация Майкрософт
author: rick-anderson
description: В предыдущих учебных курсах мы развернули наш веб-сайт, скопировав все соответствующие файлы из среды разработки в рабочую среду. Однако...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 721a5c37-7e21-48e0-832e-535c6351dcae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs
msc.type: authoredcontent
ms.openlocfilehash: 60379c87a8cf58b89066a6070ac659e65930b4fa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439014"
---
# <a name="common-configuration-differences-between-development-and-production-c"></a>Распространенные различия в конфигурации между средами разработки и производства (C#)

по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать в формате PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_cs.pdf)

> В предыдущих учебных курсах мы развернули наш веб-сайт, скопировав все соответствующие файлы из среды разработки в рабочую среду. Однако нередко возникает разница в конфигурации между средами, что требует наличия у каждой среды уникального файла Web. config. В этом учебнике рассматриваются типичные различия в конфигурации и рассматриваются стратегии обслуживания отдельных сведений о конфигурации.

## <a name="introduction"></a>Введение

В двух последних руководствах просматривается развертывание простого веб-приложения. В учебнике [*Развертывание сайта с помощью FTP-клиента*](deploying-your-site-using-an-ftp-client-cs.md) показано, как использовать АВТОНОМный FTP-клиент для копирования необходимых файлов из среды разработки в рабочую среду. Предыдущее руководство по [*развертыванию сайта с помощью Visual Studio*](deploying-your-site-using-visual-studio-cs.md)было рассмотрено в статье Развертывание с помощью средства копирования веб-сайта и публикации в Visual Studio. В обоих руководствах каждый файл в рабочей среде был копией файла в среде разработки. Однако файлы конфигурации в рабочей среде не очень часто отличаются от файлов конфигураций в среде разработки. Конфигурация веб-приложения хранится в файле `Web.config` и, как правило, содержит сведения о внешних ресурсах, таких как база данных, веб-сервер и серверы электронной почты. В нем также написано поведение приложения в определенных ситуациях, например, выполнение действий при возникновении необработанного исключения.

При развертывании веб-приложения важно, чтобы правильные сведения о конфигурации настроились в рабочей среде. В большинстве случаев файл `Web.config` в среде разработки не может быть скопирован в рабочую среду "как есть". Вместо этого необходимо отправить в рабочую среду настроенную версию `Web.config`. В этом учебнике кратко рассматриваются некоторые из наиболее распространенных различий в конфигурации. в нем также приведены некоторые методы для обслуживания различных сведений о конфигурации между средами.

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>Типичные различия конфигураций между средами разработки и рабочей средой

Файл `Web.config` содержит сведения о конфигурации для приложения ASP.NET. Некоторые из этих сведений о конфигурации одинаковы, независимо от среды. Например, параметры проверки подлинности и правила авторизации URL-адресов, написанные в `Web.config` `<authentication>` и `<authorization>`, обычно одинаковы, независимо от среды. Но другие сведения о конфигурации, такие как сведения о внешних ресурсах, обычно отличаются в зависимости от среды.

Строки подключения к базам данных — это простой пример сведений о конфигурации, которые отличаются в зависимости от среды. Когда веб-приложение обменивается данными с сервером базы данных, оно должно сначала установить соединение, которое достигается через [строку подключения](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string). Хотя можно жестко кодировать строку подключения к базе данных непосредственно на веб-страницах или в коде, который подключается к базе данных, лучше поместить его `Web.config`[элемент`<connectionStrings>`](https://msdn.microsoft.com/library/bf7sd233.aspx) , чтобы данные строки подключения находящегося в одном централизованном расположении. Часто в процессе разработки используется другая база данных, чем в рабочей среде; Следовательно, сведения о строке подключения должны быть уникальными для каждой среды.

> [!NOTE]
> В следующих учебных курсах рассматривается развертывание приложений, управляемых данными, а в этом случае мы рассмотрим особенности хранения строк подключения к базе данных в файле конфигурации.

Предполагаемое поведение сред разработки и рабочей среды существенно различается. Веб-приложение в среде разработки создается, тестируется и отлаживается небольшой группой разработчиков. В рабочей среде, в которой один и тот же приложение посещается многими пользователями одновременно. ASP.NET включает ряд функций, помогающих разработчикам в тестировании и отладке приложения, но эти функции должны быть отключены по соображениям производительности и безопасности в рабочей среде. Давайте рассмотрим несколько таких параметров конфигурации.

### <a name="configuration-settings-that-impact-performance"></a>Параметры конфигурации, влияющие на производительность

При первом посещении страницы ASP.NET (или в первый раз после ее изменения) его декларативная разметка должна быть преобразована в класс, а этот класс должен быть скомпилирован. Если веб-приложение использует автоматическую компиляцию, то также необходимо скомпилировать класс кода программной части страницы. Ассортимент параметров компиляции можно настроить с помощью [элемента`<compilation>`](https://msdn.microsoft.com/library/s10awwz0.aspx)`Web.config` файла.

Атрибут Debug является одним из наиболее важных атрибутов элемента `<compilation>`. Если для атрибута `debug` задано значение "true", скомпилированные сборки содержат отладочные символы, которые необходимы при отладке приложения в Visual Studio. Но символы отладки увеличивают размер сборки и накладывают дополнительные требования к памяти при выполнении кода. Более того, если атрибуту `debug` присвоено значение true, любое содержимое, возвращенное `WebResource.axd`, не кэшируется, то есть каждый раз, когда пользователь посещает страницу, необходимо повторно скачать статическое содержимое, возвращенное `WebResource.axd`.

> [!NOTE]
> `WebResource.axd` — это встроенный обработчик HTTP, появившийся в ASP.NET 2,0, который используется серверными элементами управления для получения внедренных ресурсов, таких как файлы скриптов, изображения, CSS-файлы и другое содержимое. Дополнительные сведения о том, как работает `WebResource.axd` и как его можно использовать для доступа к внедренным ресурсам из пользовательских серверных элементов управления, см. [в разделе доступ к внедренным ресурсам через URL-адрес с помощью `WebResource.axd`](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx).

Атрибут `debug` элемента `<compilation>` обычно имеет значение true в среде разработки. Фактически, для отладки веб-приложения этому атрибуту должно быть присвоено значение true. Если вы попытаетесь выполнить отладку приложения ASP.NET из Visual Studio, а атрибуту `debug` задано значение "false", Visual Studio отобразит сообщение о том, что приложение невозможно отладить, пока атрибуту `debug` не будет присвоено значение "true" и предложит внести это изменение.

В рабочей среде значение атрибута `debug` **не** должно быть равно "true", так как это влияет на производительность. Более подробное обсуждение этого раздела см. в записи блога [Скотта Гатри (](https://weblogs.asp.net/scottgu/), [не запуская рабочие ASP.NET приложения с включенным `debug="true"`](https://weblogs.asp.net/scottgu/442448).

### <a name="custom-errors-and-tracing"></a>Пользовательские ошибки и трассировка

При возникновении необработанного исключения в приложении ASP.NET оно переносится в среду выполнения, где происходит одно из трех действий:

- Отображается сообщение об общей ошибке среды выполнения. Эта страница информирует пользователя о том, что произошла ошибка времени выполнения, но не содержит сведений об ошибке.
- Отобразится сообщение с подробными сведениями об исключении, содержащее сведения о созданном исключении.
- Отобразится настраиваемая страница ошибки, которая представляет собой ASP.NET страницу, на которой отображается любое требуемое сообщение.

Что происходит на стороне необработанного исключения, зависит от [раздела`<customErrors>`](https://msdn.microsoft.com/library/h0hfz6fc.aspx)файла `Web.config`.

При разработке и тестировании приложения оно позволяет просматривать сведения о любом исключении в браузере. Однако отображение сведений об исключениях в приложении в рабочей среде является потенциальной угрозой безопасности. Более того, он унфлаттеринг и делает ваш веб-сайт непрофессиональным. В идеале, в случае необработанного исключения в веб-приложении в среде разработки отображаются сведения об исключении, а в том же приложении в рабочем окружении отображается настраиваемая страница ошибки.

> [!NOTE]
> Параметр раздела `<customErrors>` по умолчанию отображает сообщение сведения об исключении только в том случае, если страница посещается через localhost, и в противном случае отображается общая страница ошибки времени выполнения. Это не идеальный вариант, но мы уверены, что поведение по умолчанию не раскрывает сведения об исключении нелокальным посетителям. В следующем учебнике рассматривается раздел `<customErrors>` более подробно и показано, как при возникновении ошибки в рабочей среде отображается настраиваемая страница ошибок.

Другой компонент ASP.NET, который полезен при разработке, — это трассировка. Трассировка, если она включена, записывает сведения о каждом входящем запросе и предоставляет специальную веб-страницу `Trace.axd`для просмотра последних сведений о запросе. Вы можете включить и настроить трассировку с помощью [элемента`<trace>`](https://msdn.microsoft.com/library/6915t83k.aspx) в `Web.config`.

Если включить трассировку, убедитесь, что она отключена в рабочей среде. Поскольку данные трассировки включают файлы cookie, данные сеанса и другие потенциально конфиденциальные сведения, важно отключить трассировку в рабочей среде. Хорошая новость заключается в том, что по умолчанию трассировка отключена, а файл `Trace.axd` доступен только через localhost. Если изменить эти параметры по умолчанию в разработке, убедитесь, что они отключены в рабочей среде.

## <a name="techniques-for-maintaining-separate-configuration-information"></a>Методы обслуживания отдельных сведений о конфигурации

Наличие различных параметров конфигурации в средах разработки и рабочей среде усложняет процесс развертывания. В предыдущих двух руководствах процесс развертывания включал в себя копирование всех необходимых файлов из разработки в рабочую среду, но этот подход работает только в том случае, если информация о конфигурации одинакова в обеих средах. Существует множество методов развертывания приложения с различной информацией о конфигурации. Давайте рассмотрим некоторые из этих вариантов для размещенных веб-приложений.

### <a name="manually-deploying-the-production-environment-configuration-file"></a>Развертывание файла конфигурации рабочей среды вручную

Самый простой подход заключается в поддержке двух версий файла `Web.config`: один для среды разработки и один для рабочей среды. Развертывание сайта в рабочую среду влечет за собой копирование всех файлов на рабочий сервер в среде разработки, *за исключением* файла `Web.config`. Вместо этого файл `Web.config`, относящийся к рабочей среде, будет скопирован в рабочую среду.

Этот подход не очень сложен, но его легко реализовать, так как сведения о конфигурации изменяются редко. Он лучше всего подходит для приложений с небольшой командой разработчиков, размещенной на одном веб-сервере, и сведения о конфигурации изменяются редко. Это наиболее тенабле при ручном развертывании файлов приложения с помощью автономного FTP-клиента. При использовании средства копирования веб-сайта или варианта публикации Visual Studio необходимо сначала отфильтровать файл `Web.config`, относящийся к развертыванию, с конкретными рабочими элементами перед развертыванием, а затем поменять местами после завершения развертывания.

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>Изменение конфигурации в процессе сборки или развертывания

До сих пор предполагается, что процесс сборки и развертывания был нерегламентированным. Многие более крупные проекты программного обеспечения имеют более формальные процессы, использующие средства с открытым исходным кодом, «дома» или сторонними средствами. Для таких проектов, скорее всего, можно настроить процесс сборки или развертывания, чтобы соответствующим образом изменить сведения о конфигурации, прежде чем они будут отправлены в рабочую среду. При создании веб-приложения с помощью [MSBuild](http://en.wikipedia.org/wiki/MSBuild), [NAnt](http://nant.sourceforge.net/)или другого средства сборки, скорее всего, можно добавить шаг сборки, чтобы изменить `Web.config` файл, включив в него параметры, связанные с рабочими средами. Или рабочий процесс развертывания может программно подключиться к серверу системы управления версиями и получить соответствующий файл `Web.config`.

Фактический подход к получению соответствующих сведений о конфигурации в рабочей среде значительно зависит от ваших инструментов и рабочего процесса. Поэтому мы не будем подробно рассмотрены в этом разделе. Если вы используете популярное средство сборки, например MSBuild или NAnt, вы можете найти статьи и руководства по развертыванию, относящиеся к этим средствам, с помощью поиска в Интернете.

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>Управление различиями в конфигурации с помощью надстройки проекта веб-развертывания

В 2006 Корпорация Майкрософт выпустила надстройку проекта веб-разработки для Visual Studio 2005. Надстройка для Visual Studio 2008 была выпущена в 2008. Эта надстройка позволяет разработчикам ASP.NET создать отдельный проект веб-развертывания вместе с проектом веб-приложения, который при построении явным образом компилирует веб-приложение и копирует файлы для развертывания в локальный выходной каталог. Проект веб-приложения использует MSBuild в фоновом режиме.

По умолчанию файл `Web.config` среды разработки копируется в выходной каталог, но можно настроить проект веб-развертывания для настройки

сведения о конфигурации, которые копируются в этот каталог, можно получить следующими способами.

- С помощью команды замены раздела файла `Web.config`, в которой указывается раздел для замены, и XML-файл, содержащий замещающий текст.
- Путем указания пути к файлу внешнего источника конфигурации. Если выбран этот параметр, проект веб-развертывания копирует определенный файл `Web.config` в выходной каталог (а не на `Web.config` файл, используемый в среде разработки).
- Путем добавления настраиваемых правил в файл MSBuild, используемый проектом веб-развертывания.

Чтобы развернуть веб-приложение, выполните сборку проекта веб-развертывания, а затем скопируйте файлы из выходной папки проекта в рабочую среду.

Дополнительные сведения об использовании проекта веб-развертывания см. в [этой статье](https://msdn.microsoft.com/magazine/cc163448.aspx) , посвященной выпуску [журнала MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx)за Апрель 2007, или обратитесь к ссылкам в разделе Дополнительные материалы в конце этого руководства.

> [!NOTE]
> Нельзя использовать проект веб-развертывания с Visual Web Developer, поскольку проект веб-развертывания реализован как надстройка Visual Studio, а Visual Studio Express выпуски (включая Visual Web Developer) не поддерживают надстройки.

## <a name="summary"></a>Сводка

Внешние ресурсы и поведение веб-приложения в разработке обычно отличаются от случаев, когда одно приложение находится в рабочей среде. Например, строки подключения к базе данных, параметры компиляции и поведение при возникновении необработанного исключения обычно отличаются между средами. Процесс развертывания должен соответствовать этим различиям. Как мы обсуждали в этом руководстве, самый простой подход заключается в том, чтобы вручную скопировать альтернативный файл конфигурации в рабочую среду. Более элегантные решения можно использовать при использовании надстройки проекта веб-развертывания или в более формальном процессе сборки или развертывания, который может поддерживать такие настройки.

Поздравляем с программированием!

### <a name="further-reading"></a>Дополнительные материалы

Дополнительные сведения о разделах, обсуждаемых в этом руководстве, см. в следующих ресурсах:

- [Описание строк подключения](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [Строки подключения к базе данных @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [Не запускайте рабочие ASP.NET приложения с включенным `debug="true"`](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [Корректное реагирование на необработанные исключения — отображение понятных пользователю страниц ошибок](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [Инструкции. Использование проекта веб-развертывания Visual Studio 2008](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [Ключевые параметры конфигурации при развертывании базы данных](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Развертывание проектов веб-развертывания Visual studio 2008](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [загрузки проектов веб-развертывания Visual Studio 2005](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [Проекты веб-развертывания vs 2008](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) | [Поддержка проектов веб-развертывания VS 2008 выпущена](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [Проекты веб-развертываний](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [Назад](deploying-your-site-using-visual-studio-cs.md)
> [Вперед](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
