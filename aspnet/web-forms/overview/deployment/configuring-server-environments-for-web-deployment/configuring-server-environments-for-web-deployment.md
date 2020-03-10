---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: Настройка серверных сред для веб-развертывания | Документация Майкрософт
author: jrjlee
description: В этом учебнике показано, как настроить серверные среды для поддержки одного щелчка или автоматизированного развертывания веб-сайта и публикации в различных сцен...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 073161ce4faa3b7ba6749d7dfbaa5309eeca4f74
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515118"
---
# <a name="configuring-server-environments-for-web-deployment"></a>Настройка серверных сред для веб-развертывания

кто [Джейсон Иванов](https://github.com/jrjlee)

[Скачать в формате PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> В этом учебнике показано, как настроить серверные среды для поддержки одного щелчка или автоматизированного развертывания веб-сайта и публикации в различных сценариях. В этом учебнике содержатся разделы, посвященные выполнению различных задач, таких как Настройка веб-сервера для поддержки определенных подходов к развертыванию и настройке фермы серверов веб-фермы (WFF) вместе с обзорами на основе сценариев, которые предоставляют сквозное руководство по более высокому уровню.
> 
> В этом руководстве используется сценарий компании Fabrikam, Inc., описанный в разделе [Корпоративный веб-развертывание: обзор сценария](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) в качестве эталонной точки для примеров и сетевой инфраструктуры.
> 
> Для итальянского перевода этих руководств посетите [http://www.lucamorelli.it](http://www.lucamorelli.it).

В этом учебнике рассматриваются следующие темы:

- [Выбор правильного подхода для веб-развертывания](choosing-the-right-approach-to-web-deployment.md)
- [Сценарий. Настройка среды тестирования для веб-развертывания](scenario-configuring-a-test-environment-for-web-deployment.md)
- [Сценарий. Настройка промежуточной среды для веб-развертывания](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [Сценарий. Настройка рабочей среды для веб-развертывания](scenario-configuring-a-production-environment-for-web-deployment.md)
- [Настройка веб-сервера для публикации веб-развертывания (удаленный агент)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [Настройка веб-сервера для публикации веб-развертывания (обработчик веб-развертывания)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [Настройка веб-сервера для публикации веб-развертывания (автономное развертывание)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [Настройка сервера базы данных для публикации веб-развертывания](configuring-a-database-server-for-web-deploy-publishing.md)
- [Создание фермы серверов с помощью Web Farm Framework](creating-a-server-farm-with-the-web-farm-framework.md)
- [Настройка свойств развертывания для целевой среды](configuring-deployment-properties-for-a-target-environment.md)

Первый раздел, в котором [выбирается правильный подход к веб-развертыванию](choosing-the-right-approach-to-web-deployment.md), описывает основные подходы, которые можно использовать для публикации веб-приложений с помощью средства веб-развертывания службы IIS (IIS) (веб-развертывание) 2,0. Он также определяет сценарии, которые сопоставляются с каждым из подходов. Здесь в каждом разделе сценария представлен общий обзор задач, которые необходимо выполнить, и указаны разделы, с которыми необходимо работать для выполнения этих задач.

Если вы используете подход с файлами разделенного проекта, описанный в статье [понимание процесса сборки](../web-deployment-in-the-enterprise/understanding-the-build-process.md) для создания и развертывания решения, в последнем разделе [Настройка свойств развертывания для целевой среды](configuring-deployment-properties-for-a-target-environment.md)описано, как настроить файлы проекта конкретной среды для развертывания в различных конечных средах.

## <a name="key-technologies"></a>Ключевые технологии

В этом учебнике рассматривается использование этих продуктов и технологий для поддержки веб-развертывания.

- IIS 7,5
- Веб-развертывание 2. x
- WFF 2. x
- Служба веб-управления IIS (WMSvc)

Учебник также касается использования Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4,0 и ASP.NET MVC 3.

## <a name="other-tutorials-in-this-series"></a>Другие учебники в этой серии

Эта форма является частью серии из пяти руководств по развертыванию веб-сайта в масштабе предприятия. Ниже приведены другие руководства серии.

- [Развертывание веб-приложений в корпоративных сценариях](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Это начальное содержимое, которое содержит контекстный фон для серии руководств. В нем описывается сценарий учебника и показано, как задачи и пошаговые руководства, описанные в ряде, соответствуют более широкому процессу управления жизненным циклом приложений (ALM).
- [Веб-развертывание на предприятии](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). В этом учебнике приводятся общие сведения о файлах проекта Microsoft Build Engine (MSBuild), конвейере веб-публикации, веб-развертывание и других связанных технологиях. В нем объясняется, как можно использовать эти инструменты совместно для управления сложными процессами развертывания.
- [Настройка Team Foundation Server для веб-развертывания](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). В этом учебнике описывается настройка Team Foundation Server (TFS) для поддержки различных сценариев развертывания, включая автоматическое развертывание в рамках процесса непрерывной интеграции (CI) и запуск развертываний определенных сборок вручную.
- [Расширенное корпоративное веб-развертывание](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). В этом учебнике описывается выполнение различных более сложных задач развертывания, таких как настройка развертываний баз данных для нескольких сред, исключение файлов и папок из развертывания и перевод веб-приложений в автономный режим в процессе развертывания. .

> [!div class="step-by-step"]
> [Дальше](choosing-the-right-approach-to-web-deployment.md)
