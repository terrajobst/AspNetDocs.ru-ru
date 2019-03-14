---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: Настройка Team Foundation Server для веб-развертывание | Документация Майкрософт
author: jrjlee
description: Этом учебнике показано, как настроить Team Foundation Server (TFS) 2010 для создания решений и развертывания веб-содержимого для различных целевых средах. Это...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2b668f2e9bdf73632b8b076416c9ccc5cf34a7ed
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058831"
---
<a name="configuring-team-foundation-server-for-web-deployment"></a>Настройка Team Foundation Server для веб-развертывания
====================
по [Джейсон Lee](https://github.com/jrjlee)

[Загрузить PDF-файл](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Этом учебнике показано, как настроить Team Foundation Server (TFS) 2010 для создания решений и развертывания веб-содержимого для различных целевых средах. Сюда входят сценарии непрерывной интеграции (CI), где при развертывании содержимого автоматически каждый раз, когда разработчик вносит изменение. Оно также может включать ручной запуск сценариев, где администратор может потребоваться активировать развертывание для определенной сборки в среде промежуточного хранения в том случае, когда сборка будет проверено и проверен в тестовой среде. Разделы в данном руководстве поможет процесса настройки, включая:
> 
> - Как создать новый командный проект в Team Foundation Server.
> - Как добавить содержимое в систему управления версиями.
> - Сведения о настройке сервера сборки для поддержки непрерывной Интеграции и развертывания.
> - Как создать определение сборки, которое использует логику развертывания.
> - Сведения о настройке разрешений для автоматического развертывания.
> 
> Итальянский перевода учебников, см. в статье [ http://www.lucamorelli.it ](http://www.lucamorelli.it).


Предполагается, что вы установили TFS 2010 и создания коллекции командных проектов в рамках процесса начальной настройки. [Руководство по установке Team Foundation для Visual Studio 2010](https://go.microsoft.com/?linkid=9805132) представлены обширные инструкции об этих задачах.

## <a name="context"></a>Контекст

Это является частью серии учебников, в соответствии с требованиями развертывания enterprise для вымышленной компании Fabrikam, Inc. В этой серии руководств используется пример решения&#x2014; [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) решение&#x2014;для представления веб-приложения с более реалистичные уровень сложности, включая приложения ASP.NET MVC 3, Windows Communication Служба Foundation (WCF) и проект базы данных.

Метод развертывания в основе этих учебников основан на разбиение проекта файл подход, описанный в [основные сведения о процессе построения](../web-deployment-in-the-enterprise/understanding-the-build-process.md), в которой процесс построения управляется двумя файлы проекта&#x2014;один с Создание инструкции, которые применяются для каждой целевой среде и содержащего параметры построения и развертывания для конкретной среды. Во время сборки файл проекта для конкретной среды объединяется в файл проекта независимой от среды, чтобы полный набор инструкций построения.

## <a name="scenario-overview"></a>Общие сведения о сценарии

Сценарий верхнего уровня в этих руководствах описывается в [корпоративное веб-развертывание: Обзор сценария](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md). Рекомендуется просмотреть в этом разделе, прежде чем приступить к работе в этом руководстве.

## <a name="how-to-use-this-tutorial"></a>Как использовать этот учебник

Если это первый случай выполнения задач, описанных в этом руководстве, или если вы хотите выполнить примеры, используя пример решения, следует выполнить разделы учебника в порядке. Кроме того как рекомендации можно использовать отдельные разделы для конкретных задач. Этот учебник содержит следующие разделы:

- [Создание командного проекта в Team Foundation Server](creating-a-team-project-in-tfs.md). Командный проект является основной единицей для системы управления версиями, управления процессами и сборки в TFS. Необходимо создать командный проект, прежде чем добавлять содержимое в систему управления версиями или создание определений сборок.
- [Добавление содержимого в систему управления версиями](adding-content-to-source-control.md). После создания командного проекта, можно начать добавлять содержимое в систему управления версиями. Необходимо добавить проектов и решений, а также любых внешних зависимостей, перед началом настройки построений.
- [Настройка TFS сервер сборки для развертывания веб-](configuring-a-tfs-build-server-for-web-deployment.md). Если вы хотите создавать содержимое командного проекта, необходимо настроить сервер сборки. В большинстве случаев это должно быть на отдельном компьютере из установки TFS. Чтобы настроить сервер сборки, вам потребуется установка и настройка службы сборок TFS, установите Visual Studio 2010, создать контроллеры построений и агенты сборки, установить все продукты и компоненты, необходимые для успешной сборки и установки кода Internet Information Services (IIS) средство веб-развертывания (веб-развертывания).
- [Создание определения сборки, которая поддерживает развертывание](creating-a-build-definition-that-supports-deployment.md). Прежде чем приступить к очереди или активации сборок в Team Foundation Server, необходимо создать по крайней мере одно определение сборки для командного проекта. Определения построения определяет все аспекты сборки, включая какие действия должны быть включены в построение, какие события должны запускать сборки и где Team Build следует отправлять выходные данные сборки. Можно настроить определение сборки для запуска пользовательских файлов проекта Microsoft Build Engine (MSBuild), позволяющий включать логики развертывания в автоматических построениях.
- [Развертывание конкретной сборки](deploying-a-specific-build.md). В большинстве сценариев нужно будет развернуть определенной сборки, а не в последней сборке, к целевой среде. В этом случае можно настроить определение сборки, который развертывает содержимое из папки сброса, определенного.
- [Настройка разрешений для группы развертывания построения](configuring-permissions-for-team-build-deployment.md). Если служба сборки для развертывания содержимого как часть автоматизированного процесса сборки, необходимо предоставить различные разрешения для учетной записи службы сборки на любой целевой веб-серверов и серверов баз данных.

## <a name="key-technologies"></a>Ключевые технологии

Это руководство посвящено как использовать эти продукты и технологии для поддержки автоматической сборки и развертывания веб-приложения:

- Visual Studio Team Foundation Server 2010
- Team Build и MSBuild
- Web Deploy

При использовании Windows Server 2008 R2, IIS 7.5, SQL Server 2008 R2, ASP.NET 4.0 и ASP.NET MVC 3 также касается руководства.

## <a name="other-tutorials-in-this-series"></a>Другие руководства в этой серии

Это формирует части серии из пяти учебников на веб-развертывание в масштабах предприятия. Ниже приведены другие руководства в серии.

- [Развертывание веб-приложений в корпоративных сценариях](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Вводные представлены контекстные фона для этой серии руководств. Здесь описываются рассматриваемый сценарий, а его показано, как задачи и пошаговые руководства, описанные на протяжении ряда помещается в более широкого процесса управления жизненным циклом приложений (ALM).
- [Веб-развертывания на предприятии](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Этот учебник содержит общие сведения о файлах проекта MSBuild, конвейер публикации Web (WPP), веб-развертывания и других связанных технологий. Здесь объясняется, как можно использовать эти средства вместе для управления процессами сложного развертывания.
- [Настройка серверных сред для веб-развертывания](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md). Это руководство содержит инструкции для настройки серверов Windows для поддержки различных сценариев развертывания, включая развертывания удаленного веб-пакета, используя службу агента веб-развертывания (удаленный агент) или веб-обработчик развертывания и удаленной базы данных развертывания. Он содержится руководство по выбору соответствующий метод развертывания для конкретной среды, и описано, как использовать веб-фермы (WFF) для репликации развернутых веб-приложений на веб-серверов в ферме серверов.
- [Advanced корпоративное веб-развертывание](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). Это руководство содержит инструкции по выполнению различных задач более сложные развертывания, такие как настройка развертываний баз данных для нескольких сред, исключение файлов и папок из развертывания и получение веб-приложений в автономный режим во время развертывания .

> [!div class="step-by-step"]
> [Вперед](creating-a-team-project-in-tfs.md)