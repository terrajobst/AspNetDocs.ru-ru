---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: Веб-развертывания на предприятии | Документация Майкрософт
author: jrjlee
description: Это руководство содержит инструкции для удовлетворения множество задач, с которыми придется столкнуться при управлении развертыванием веб-приложений корпоративного уровня для разраб...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: 735cc5ac37e369e6149c526174c3f74a08db9758
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026161"
---
<a name="web-deployment-in-the-enterprise"></a>Корпоративное веб-развертывание
====================
по [Джейсон Lee](https://github.com/jrjlee)

[Загрузить PDF-файл](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Это руководство содержит инструкции для удовлетворения множество задач, с которыми придется столкнуться при управлении развертыванием веб-приложений корпоративного уровня для разработки, тестирования, промежуточной и рабочей средах. Учебник включает эталонного решения, а также сочетание концептуальные и ориентированные на задачи содержимого, которые описывают различные стандартные задачи и процедуры.
> 
> Итальянский перевода учебников, см. в статье [ http://www.lucamorelli.it ](http://www.lucamorelli.it).


## <a name="enterprise-deployment-challenges"></a>Трудности при развертывании Enterprise

Организациям часто возникают эти трудности при они выглядят для развертывания сложных решений корпоративного уровня:

- Необходимо иметь возможность развертывать проекты в нескольких средах, таких как разработчик или тестовых сред, промежуточные платформ и рабочих серверах. Решение необходимо развертывать с помощью параметров конфигурации для каждой среды.
- В этом случае необходимо выполнить развертывание несколькими зависимыми проектами одновременно в рамках один шаг или автоматического процесса построения и развертывания.
- Необходимо иметь возможность развертывания диск из автоматизированного процесса. Например вы хотите использовать процесс непрерывной интеграции (CI) для развертывания веб-приложений в тестовой среде, при возврате нового кода.
- Необходимо иметь возможность контролировать процесс развертывания и установки переменных развертывания вне Visual Studio, как разработчики будут иметь правильные настройки или необходимые учетные данные для каждой целевой среды.
- Необходимо развертывать проекты на основе схемы базы данных и сохранить существующие данные при последующих развертываниях.
- Необходимо выполнить развертывание базы данных членства на нерегламентированные без развертывания данных учетной записи пользователя. Также может потребоваться обновить схему баз данных развернутого членства без потери существующих данных учетной записи пользователя.
- Необходимо исключить определенные файлы или папки, при развертывании содержимого в различных целевых средах.

## <a name="overview-of-approach"></a>Общие сведения о подходе

Этом руководстве, а также другие руководства в этой серии используется общий подход для решения этих проблем, описанных выше.

- **Используйте пользовательские файлы проекта Microsoft Build Engine (MSBuild) для управления общий процесс сборки и развертывания.**
- Это позволяет вам создавать и развертывать каждый проект в решении в рамках одной операции с поддержкой сценариев.
- Параметры, относящиеся к среде настраиваются с помощью файлов простого проекта для конкретной среды. В отличие от Visual Studio ориентированный подход с использованием конфигурации решения и профилей публикации для настройки развертываний для разных сред, такой подход позволяет настраивать и управлять процессом развертывания вне Visual Studio. Это означает, что разработчики не должны Расширьте знания о строки подключения, конечные точки службы, учетные данные сервера и другие переменные развертывания для целевой среды.
- Файлы проектов могут вызываться в Team Build в рамках процесса Team Foundation Server (TFS). Вы можете настроить автоматическое развертывание для сценариев непрерывной Интеграции.

**Используйте средство Internet Information Services (IIS) веб-развертывания (веб-развертывание) для упаковки и развертывания проектов веб-приложений.**

- Веб-развертывание предоставляет платформу, которая позволяет упаковать и развернуть веб-приложение содержимого целевой веб-сервер IIS, а также зависимости, параметры конфигурации, параметры безопасности и прочие требования.
- Вы можете управлять весь процесс упаковки и развертывания из пользовательских файлов проекта MSBuild. Можно управлять параметрами конфигурации, сопровождающих пакет веб-развертывания, например строки подключения, конечные точки службы и сведения о назначении IIS.
- Веб-развертывание, а также конвейера публикации в Интернете, дает множество точек расширения, которые позволяют настраивать развертывание. Например это легко исключить ненужные файлы и папки из вашей веб-развертывания пакетов.

**Программа VSDBCMD.exe для развертывания и обновления схемы баз данных.**

- Средство VSDBCMD можно развернуть базы данных из файла схемы базы данных (с расширением DBSCHEMA), который создается при построении проекта базы данных Visual Studio. В противоположность этому функции развертывания базы данных, включенные в веб-развертывания — больше всего подходит развертывания существующих баз данных из локального экземпляра SQL Server.
- В отличие от функции Visual Studio для развертывания проектов баз данных средство VSDBCMD позволяет развертывать разностные обновления существующей целевой базы данных. Это позволяет сохранить все существующие данные при обновлении схемы базы данных.
- Позволяет выполнять команды VSDBCMD из пользовательских файлов проекта MSBuild.

## <a name="content-map"></a>Карта содержимого

Этот учебник содержит разделы, которые делятся на четыре основных области.

В этих разделах вводят эталонного решения&#x2014;решения диспетчера контактов&#x2014;и описывается, как загрузить и настроить его на локальном компьютере:

- [Решение диспетчера контактов](the-contact-manager-solution.md)
- [Настройка решения диспетчера контактов](setting-up-the-contact-manager-solution.md)

В этих разделах вводите файлы проекта MSBuild, описывают, как создать и использовать файлы пользовательского проекта и ознакомьтесь с процессом развертывания для решения диспетчера контактов:

- [Общие сведения о файле проекта](understanding-the-project-file.md)
- [Общие сведения о процессе сборки](understanding-the-build-process.md)

В этих разделах описывается развертывание веб-приложений, включая том, как сборки и упаковки процесс, как процесс построения интегрируется с конвейера публикации в Интернете, изменение параметров развертывания и развертывание веб-пакетов в место назначения среды:

- [Сборка и упаковка проектов веб-приложений](building-and-packaging-web-application-projects.md)
- [Настройка параметров для развертывания веб-пакета](configuring-parameters-for-web-package-deployment.md)
- [Развертывание веб-пакетов](deploying-web-packages.md)

- [Развертывание проектов базы данных](deploying-database-projects.md) описывает различные методы можно использовать для развертывания проектов баз данных Visual Studio, а также преимущества и недостатки каждого подхода. [Создание и запуск командного файла развертывания](creating-and-running-a-deployment-command-file.md) описывается создание простого командный файл, который содержит логику развертывания и позволяет развертывать сложные решения как один шаг процесса.
- Наконец [вручную Установка веб-пакеты](manually-installing-web-packages.md) завершает учебник, отображая сведения для импорта веб-пакетов в IIS.

## <a name="key-technologies"></a>Ключевые технологии

Подразделы в этом руководстве в первую очередь использовать эти технологии для управления сборки и развертывания:

- Visual Studio 2010
- MSBuild
- IIS 7.5
- Web Deploy 2.0
- Программа развертывания VSDBCMD.exe базы данных

## <a name="other-tutorials-in-this-series"></a>Другие руководства в этой серии

Это формирует части серии из пяти учебников на веб-развертывание в масштабах предприятия. Ниже приведены другие руководства в серии.

- [Развертывание веб-приложений в корпоративных сценариях](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Вводные представлены контекстные фона для этой серии руководств. Здесь описываются рассматриваемый сценарий, а его показано, как задачи и пошаговые руководства, описанные на протяжении ряда помещается в более широкого процесса управления жизненным циклом приложений (ALM).
- [Настройка серверных сред для веб-развертывания](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). Это руководство содержит инструкции для настройки серверов Windows для поддержки различных сценариев развертывания, включая развертывания удаленного веб-пакета, используя службу агента веб-развертывания (удаленный агент) или веб-обработчик развертывания и удаленной базы данных развертывания. Он содержится руководство по выбору соответствующий метод развертывания для конкретной среды, и описано, как использовать веб-фермы (WFF) для репликации развернутых веб-приложений на веб-серверов в ферме серверов.
- [Настройка Team Foundation Server для развертывания веб-](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). Это руководство содержит инструкции для настройки TFS для поддержки различных сценариев развертывания, включая автоматическое развертывание в рамках процесса непрерывной Интеграции и запущено развертывание определенных сборок вручную.
- [Advanced корпоративное веб-развертывание](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). Это руководство содержит инструкции по выполнению различных задач более сложные развертывания, такие как настройка развертываний баз данных для нескольких сред, исключение файлов и папок из развертывания и получение веб-приложений в автономный режим во время развертывания .

> [!div class="step-by-step"]
> [Вперед](the-contact-manager-solution.md)