---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
title: Распространенные различия в конфигурации между средами разработки и производства (Visual Basic) | Документация Майкрософт
author: rick-anderson
description: В предыдущих учебных курсах мы развернули наш веб-сайт, скопировав все необходимые файлы из среды разработки в рабочую среду. Тем не менее я...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 548e75f6-4d6c-4cb4-8da8-417915eb8393
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
msc.type: authoredcontent
ms.openlocfilehash: ec1d575fac4527db8f5bcab5f0d84e1f17eac46b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048781"
---
<a name="common-configuration-differences-between-development-and-production-vb"></a>Распространенные различия в конфигурации между средами разработки и производства (VB)
====================
по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Загрузить PDF-файл](http://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_vb.pdf)

> В предыдущих учебных курсах мы развернули наш веб-сайт, скопировав все необходимые файлы из среды разработки в рабочую среду. Тем не менее это не часто бывает различия конфигурации между средами, которые требуется открытое, у вас есть уникальный файл Web.config для каждой среды. Этом руководстве рассматриваются различия в стандартной конфигурации и рассматривает стратегии обеспечения сведения о конфигурации отдельных.


## <a name="introduction"></a>Вступление


Последних двух учебных приведены пошаговые инструкции по развертыванию простого веб-приложения. [ *Развертывание сайта с помощью FTP-клиент* ](deploying-your-site-using-an-ftp-client-vb.md) учебнике было показано, как использовать автономный клиент FTP скопировать необходимые файлы из среды разработки до производства. Предыдущем учебном курсе, [ *развертывание Your сайта с помощью Visual Studio*](deploying-your-site-using-visual-studio-vb.md), рассмотрены развертывание с помощью средства копирования веб-сайта и публикации Visual Studio. В обоих учебников каждый файл в рабочей среде была копия файла в среде разработки. Тем не менее это не часто файлы конфигурации в рабочей среде, чтобы отличаться от показанных в среде разработки. Конфигурация веб-приложение хранится в `Web.config` файл, а также обычно включает сведения о внешних ресурсов, таких как базы данных, Интернета и серверы электронной почты. Он также устанавливает поведение приложения в определенных ситуациях, например действие, выполняемое при возникновении необработанного исключения.

При развертывании веб-приложения очень важно, что необходимая информация в итоге в рабочей среде. В большинстве случаев `Web.config` не удается скопировать файл в среде разработки в рабочей среде, что-является. Вместо этого настроенную версию `Web.config` , необходимо передать в рабочей среде. Этот учебник кратко рассматриваются некоторые из наиболее распространенных различия в конфигурации; Он также содержатся некоторые методы обеспечения различные сведения о конфигурации между средами.

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>Различия в стандартной конфигурации разработки и рабочей среды

`Web.config` Файл, содержащий набор сведений о конфигурации для приложения ASP.NET. Некоторые из этих сведений конфигурации не зависит от среды. Например, параметры проверки подлинности и правила авторизации URL-адрес, выраженная в `Web.config` файла `<authentication>` и `<authorization>` элементы обычно такие же, независимо от среды. Но обычно других сведений о конфигурации — например, сведения о внешних ресурсах - отличается в зависимости от среды.

Строки подключения к базам данных — это отличный пример параметров конфигурации, которая отличается от среды. Когда веб-приложение связывается с сервером базы данных, его необходимо сначала установить соединение, и который достигается за счет [строку подключения](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string). Хотя можно жестко строку подключения базы данных непосредственно в веб-страниц или код, который подключается к базе данных, лучше поместить его `Web.config` [ `<connectionStrings>` элемент](https://msdn.microsoft.com/library/bf7sd233.aspx) таким образом, чтобы строка подключения информация находится в одного централизованного расположения. Очень часто использовать другую базу данных во время разработки не используется в рабочей среде; Следовательно данные строки подключения должно быть уникальным для каждой среды.

> [!NOTE]
> Последующих учебных курсах изучение, развертывание приложений, управляемых данными, после чего мы подробно рассмотрим особенности хранение строк подключений баз данных в файле конфигурации.


Предполагаемое поведение среды разработки и эксплуатации значительно отличается. Веб-приложения в среде разработки создается, тестирования и отладки с небольшой группой разработчиков. В рабочей среде, что посещений того же приложения с множеством разных одновременно работающих пользователей. ASP.NET включает ряд функций, помогающих разработчикам при тестировании и отладке приложения, но эти функции должен быть отключен для производительности и по соображениям безопасности при работе в рабочей среде. Давайте рассмотрим несколько такие параметры конфигурации.

### <a name="configuration-settings-that-impact-performance"></a>Параметры конфигурации, влияющие на производительность

При посещении страницы ASP.NET в первый раз (или в первый раз после его изменения), необходимо преобразовать его декларативная разметка в класс, и этот класс должен быть скомпилирован. Если веб-приложение использует автоматическую компиляцию кода классов страницы должен быть скомпилирован, слишком. Можно настроить различные параметры компиляции с помощью `Web.config` файла [ `<compilation>` элемент](https://msdn.microsoft.com/library/s10awwz0.aspx).

Атрибут debug является одним из наиболее важных атрибутов в `<compilation>` элемент. Если `debug` атрибут имеет значение «true», а затем скомпилированные сборки содержатся символы отладки, которые нужны при отладке приложения в Visual Studio. Но отладочные символы увеличивают размер сборки и наложить дополнительные требования к памяти при выполнении кода. Кроме того, когда `debug` атрибут имеет значение «true» любое содержимое, возвращенный `WebResource.axd` не кэшируется, то есть каждый раз пользователь посещает страницу, им необходимо будет повторно загрузить статическое содержимое, возвращенный `WebResource.axd`.

> [!NOTE]
> `WebResource.axd` Встроенный обработчик HTTP появилась в ASP.NET 2.0, использовать серверные элементы управления для извлечения внедренных ресурсов, таких как файлы скриптов, изображений, файлов CSS и другое содержимое. Дополнительные сведения о том, как `WebResource.axd` работает и как ее можно использовать для доступа к внедренных ресурсов из пользовательских серверных элементов управления, см. в разделе [доступ к внедренных ресурсов через URL-адрес с помощью `WebResource.axd` ](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx).


`<compilation>` Элемента `debug` атрибут обычно имеет значение «true» в среде разработки. На самом деле, этот атрибут необходимо быть значение «true», чтобы выполнять отладку веб-приложения; При попытке отладить приложение ASP.NET из Visual Studio и `debug` атрибут имеет значение «false», Visual Studio отобразит сообщение о том, что приложение не может быть отлажен до `debug` атрибут имеет значение «true» и будет предложение, чтобы внести это изменение автоматически.

Вы должны **никогда не** имеют `debug` набором атрибутов «true» в рабочей среде из-за его влияния на производительность. Более подробное обсуждение по этой теме, см. в разделе [Скотт Гатри](https://weblogs.asp.net/scottgu/)в записи блога, [не запуска рабочей среде ASP.NET приложений с `debug="true"` включено](https://weblogs.asp.net/scottgu/442448).

### <a name="custom-errors-and-tracing"></a>Пользовательские ошибки и трассировка

При возникновении необработанного исключения в приложении ASP.NET она поднимается среды выполнения, после чего происходит одно из трех действий:

- Отображается сообщение об ошибке универсального среды выполнения. Эта страница пользователю о том, что была ошибка времени выполнения, но не предоставляет все сведения об ошибке.
- Отображается сообщение сведения об исключении, который включает информацию на исключение, выданное просто.
- Отображается на пользовательскую страницу ошибки, который является страница ASP.NET, созданный, которая отображает все сообщения, которые необходимы.

Что происходит при возникновении необработанного исключения зависит от `Web.config` файла [ `<customErrors>` разделе](https://msdn.microsoft.com/library/h0hfz6fc.aspx).

При разработке и тестировании приложения, он позволяет просматривать сведения о любое исключение, в браузере. Тем не менее показывающий сведения об исключении в приложение на рабочих является потенциальную угрозу безопасности. Кроме того она unflattering и предоставляет веб-сайт выглядеть непрофессионально. В идеале в случае необработанного исключения веб-приложения в среде разработки будет отображается сведения об исключении, тогда как одного приложения в рабочей среде будут отображаются на пользовательскую страницу ошибки.

> [!NOTE]
> Значение по умолчанию `<customErrors>` параметр раздела показаны сведения об исключении сообщение только в том случае, когда страница посещается через localhost и в противном случае отображается страница ошибки универсального среды выполнения. Это не лучший вариант, но он обеспечение знать поведение по умолчанию не поможет найти сведения об исключении для нелокальных посетителей. Проверяет следующем учебном курсе `<customErrors>` разделе более подробно и показано, как у на пользовательскую страницу ошибки показано при возникновении ошибки в рабочей среде.


Еще одна функция ASP.NET, полезно использовать во время разработки трассировки. Трассировки, если параметр включен, записывает сведения о каждого входящего запроса и предоставляет специальный веб-страницы, `Trace.axd`, для просмотра последних сведений о запросе. Можно включить и настроить трассировку с помощью [ `<trace>` элемент](https://msdn.microsoft.com/library/6915t83k.aspx) в `Web.config`.

При включении трассировки убедитесь, что он отключен в рабочей среде. Сведения о трассировке включает файлы cookie, данные о сеансе и других потенциально конфиденциальная информация, очень важно отключить трассировку в рабочей среде. Хорошая новость состоит в том, что, по умолчанию трассировка отключена и `Trace.axd` файл доступен только через localhost. Если изменить эти параметры по умолчанию в разработке убедитесь, что они отключены обратно в рабочей среде.

## <a name="techniques-for-maintaining-separate-configuration-information"></a>Сведения о конфигурации отдельных методов

Наличие параметров конфигурации в средах разработки и эксплуатации усложняет процесс развертывания. В двух предыдущих учебных процесс развертывания включал в себя копирование все необходимые файлы из среды разработки в рабочей среде, но этот подход работает, только если сведения о конфигурации одинакова в обеих средах. Существуют различные методы для развертывания приложения с различной информацией о конфигурации. Давайте каталога некоторые из этих параметров для размещенного веб-приложений.

### <a name="manually-deploying-the-production-environment-configuration-file"></a>Развертывание вручную в файле конфигурации рабочей среды

Самый простой подход заключается в поддержке две версии `Web.config` файла: один для среды разработки и один для рабочей среды. Развертывание узла в рабочей среде влечет за собой копирование всех файлов на рабочий сервер в среде разработки *за исключением* для `Web.config` файла. Вместо этого конкретной среды производственного `Web.config` файл будет скопирован в рабочую среду.

Этот подход не является очень сложна, но это легко реализовать, так как сведения о конфигурации изменяются редко. Она лучше всего подходит для приложений с помощью небольшая команда разработчиков, которые размещаются на одном сервере и редко изменяется, сведения о конфигурации. Это наиболее tenable при ручном развертывании файлы приложения с помощью автономного клиента FTP. При использовании средства копирования веб-сайта или публикации Visual Studio необходимо сначала заменить относящиеся к развертыванию `Web.config` файла с той, относящиеся к рабочей среде перед развертыванием и заменять их обратно после завершения развертывания.

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>Изменение конфигурации во время сборки или процесс развертывания

До сих обсуждения предполагается процесса построения и развертывания ad-hoc. Многие крупные проекты программного обеспечения более формализации процессы, которые делают использование открытым кодом, — громоздких, или сторонние средства. Скорее всего, для таких проектов можно настроить процесс сборки или развертывания, чтобы соответствующим образом изменить сведения о конфигурации, перед отправкой в рабочую среду. При построении вашего веб-приложения с помощью [MSBuild](http://en.wikipedia.org/wiki/MSBuild), [NAnt](http://nant.sourceforge.net/), или другого средства построения, скорее всего добавить шаг сборки, чтобы изменить `Web.config` файл, чтобы включить параметры, относящиеся к рабочей среде. Или рабочий процесс развертывания может программным способом подключения для сервера системы управления версиями и получения соответствующего `Web.config` файл.

Фактический подход для получения сведений о соответствующей конфигурации в рабочей среде зависит от широко средства и рабочий процесс. Таким образом мы не будет углубимся в этом разделе. Если вы используете средства построения популярных как MSBuild или NAnt можно найти развертывания статьи и учебники относятся к следующим средствам через веб-поиска.

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>Управление различия в конфигурации с помощью веб-развертывания проекта надстройки

В 2006 г. Корпорация Майкрософт выпустила веб-разработки проекта надстроек для Visual Studio 2005. Надстройки для Visual Studio 2008 была выпущена в 2008 г. Эта надстройка позволяет разработчикам ASP.NET для создания отдельных веб-проекта развертывания вместе с их проекта веб-приложения, при построении, явно компилирует веб-приложения и копирует файлы для развертывания локального выходного каталога. Проект веб-приложения использует MSBuild в фоновом.

По умолчанию в среде разработки `Web.config` файл копируется в выходной каталог, но вы можете настроить веб-проекта развертывания для настройки

сведения о конфигурации, который копируется в этот каталог одним из следующих способов:

- С помощью `Web.config` файла замены раздела, в котором указываются разделе, чтобы заменить и XML-файл, содержащий текст замены.
- Нужно указать путь к файлу конфигурации внешнего источника. Этот параметр выбран, проект веб-развертывания копирует определенный `Web.config` файл в выходной каталог (а не `Web.config` файл, используемый в среде разработки).
- Путем добавления настраиваемых правил в файл MSBuild, используемые веб-проекта развертывания.

Для развертывания сборки приложения web проект веб-развертывания и скопируйте файлы из папки выходных данных проекта в рабочую среду.

Дополнительные сведения об использовании веб-развертывания проекта см [в этой статье Web Deployment Projects](https://msdn.microsoft.com/magazine/cc163448.aspx) из за апрель 2007 года [журнала MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx), или обратитесь к ссылкам в раздел «Дополнительные материалы» конце этого руководства.

> [!NOTE]
> Проект веб-развертывания нельзя использовать с Visual Web Developer, так как проект веб-развертывания реализуется как Visual Studio Add-In и Visual Studio Express Editions (включая Visual Web Developer) не поддерживают надстройки.


## <a name="summary"></a>Сводка

Внешние ресурсы и поведение веб-приложения в разработке обычно отличаются от при того же приложения в рабочей среде. Например строки подключения к базам данных, параметры компиляции и поведение при возникновении необработанного исключения, обычно отличаются между средами. Процесс развертывания необходимо принять во внимание эти различия. Как уже говорилось, в этом руководстве, самым простым подходом является вручную скопировать файл альтернативную конфигурацию в рабочей среде. Возможны более элегантные решения при использовании веб-развертывания проекта надстроек или с более Формализованная процессом сборки или развертывания, который способен обрабатывать такие настройки.

Счастливого вам программирования!

### <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения по темам, обсуждавшимся в этом руководстве см. в следующих ресурсах:

- [Описано строки подключения](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [@ ConnectionStrings.com строки подключения базы данных](http://www.connectionstrings.com/)
- [Не запускать рабочие приложения ASP.NET с помощью `debug="true"` включена](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [Корректно отвечать на необработанные исключения - отображение понятных ошибки страниц](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [Инструкции: Использовать проект развертывания веб-Visual Studio 2008?](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [Параметры конфигурации с ключом, при развертывании базы данных](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Загрузка проектов Visual Studio 2008 Web Deployment](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [загрузки проектов развертывания Visual Studio 2005](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [VS 2008 Web Deployment Projects](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) | [поддержка VS 2008 веб-развертывания проектов с выпуска](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [Проекты веб-развертываний](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [Назад](deploying-your-site-using-visual-studio-vb.md)
> [Вперед](core-differences-between-iis-and-the-asp-net-development-server-vb.md)