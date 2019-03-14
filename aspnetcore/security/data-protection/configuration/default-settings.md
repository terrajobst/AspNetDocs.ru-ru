---
title: Управление ключами для защиты данных и время существования в ASP.NET Core
author: rick-anderson
description: Дополнительные сведения об управлении ключами для защиты данных и время существования в ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/configuration/default-settings
ms.openlocfilehash: 2f022a4c7519485fe629ce47c27d214c8c27d5bc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036561"
---
# <a name="data-protection-key-management-and-lifetime-in-aspnet-core"></a>Управление ключами для защиты данных и время существования в ASP.NET Core

Автор: [Рик Андерсон](https://twitter.com/RickAndMSFT) (Rick Anderson)

## <a name="key-management"></a>Управление ключами

Приложение пытается обнаружить операционной среды и обработать конфигурацию ключа сам по себе.

1. Если приложение будет размещено в [приложений Azure](https://azure.microsoft.com/services/app-service/), ключи сохраняются в *%HOME%\ASP.NET\DataProtection-Keys* папки. Эта папка копируется в сетевое хранилище и синхронизируется на всех машинах, где размещается приложение.
   * Во время хранения ключи не защищаются.
   * *DataProtection ключи* папке хранится связка ключей для всех экземпляров приложения в одного слота развертывания.
   * Отдельные слоты развертывания, такие как промежуточное хранение и производство, не используют общую связку ключей. При переключении между слотами развертывания, пример переключения промежуточной в рабочую среду или с помощью A / B-тестирования, любое приложение, с помощью защиты данных не сможет расшифровать хранимые данные, используя связку ключей из предыдущего слота. Это приводит к пользователям вышли из приложения, которое использует стандартную проверку подлинности файла cookie ASP.NET Core, так как он использует защиту данных для защиты файлов cookie. При желании колец ключ независимый от слота, используйте внешнего поставщика связки ключей, такие как хранилище BLOB-объектов Azure, хранилище ключей Azure, в хранилище SQL или кэша Redis.

1. Если профиль пользователя, ключи сохраняются в *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* папки. Если операционная система Windows, они шифруются при хранении с помощью DPAPI.

   Также необходимо включить атрибут [setProfileEnvironment](/iis/configuration/system.applicationhost/applicationpools/add/processmodel#configuration) пула приложений. Значением свойства `setProfileEnvironment` по умолчанию является `true`. В некоторых сценариях (например, в ОС Windows) для параметра `setProfileEnvironment` установлено значение `false`. Если ключи не хранятся в каталоге профиля пользователя:

   1. Перейдите к папке *%windir%/system32/inetsrv/config*.
   1. Откройте файл *applicationHost.config*.
   1. Найдите элемент `<system.applicationHost><applicationPools><applicationPoolDefaults><processModel>` .
   1. Убедитесь, что атрибут `setProfileEnvironment` отсутствует и установлено значение по умолчанию `true`, или же явно задайте для атрибута значение `true`.

1. Если приложение размещается в службах IIS, ключи сохраняются в реестре HKLM, в специальный раздел, который будет доступен только для учетной записи рабочего процесса. Неактивные ключи шифруются с помощью API защиты данных.

1. Если ни один из этих условий, ключи не сохраняются за пределами текущего процесса. Когда процесс завершится, все созданные ключи будут потеряны.

Разработчик получает полный контроль над всегда и можно переопределить, как и где хранятся ключи. Первые три параметра выше должен предоставлять по умолчанию для большинства приложений, подобно тому, как ASP.NET  **\<machineKey >** подпрограммы автоматическое создание работал в прошлом. Последний, резервный параметр — единственный сценарий, разработчик должен указать [конфигурации](xref:security/data-protection/configuration/overview) переднего плана, если им нужен постоянство ключа, но этот откат происходит только в редких случаях.

При размещении в контейнере Docker, ключи должны сохраняться в папку, которая является томом Docker (общего тома или узла подключенном томе, который сохраняется вне пределов продолжительности контейнера) или во внешнем поставщике, такие как [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) или [Redis](https://redis.io/). Внешнего поставщика также полезно в сценариях веб-ферм, если приложения нет доступа к общей сетевой том (см. в разделе [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) Дополнительные сведения).

> [!WARNING]
> Если разработчик переопределяет правилам, описанным выше и указывает системы защиты данных в определенных репозиториях ключа, будет отключено автоматическое шифрование ключей при хранении. Защита неактивных данных можно будет снова включить с помощью [конфигурации](xref:security/data-protection/configuration/overview).

## <a name="key-lifetime"></a>Время жизни ключа

По умолчанию ключи имеют срок действия 90 дней. По истечении срока действия ключа приложение автоматически создает новый ключ и задает в качестве активного ключа новый ключ. До тех пор, пока удалено ключи остаются в системе, приложение может расшифровать все данные, защищенные с ними. См. в разделе [управление ключами](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) Дополнительные сведения.

## <a name="default-algorithms"></a>Алгоритмы по умолчанию

Используемый алгоритм защиты полезных данных по умолчанию — AES-256-CBC по конфиденциальности и HMACSHA256 подлинность. Главный ключ 512-разрядных, изменить каждые 90 дней, используется для формирования двух вложенных ключей, используемых для этих алгоритмов по принципу в полезных данных. См. в разделе [подраздел наследования](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) Дополнительные сведения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* <xref:security/data-protection/extensibility/key-management>
* <xref:host-and-deploy/web-farm>