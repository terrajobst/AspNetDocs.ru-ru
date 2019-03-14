---
title: Управление ключами в ASP.NET Core
author: rick-anderson
description: Дополнительные сведения о реализации API защиты данных в ASP.NET Core ключа управления.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-management
ms.openlocfilehash: 431bdf2d3076c83279b78f327ddb647f69e6e584
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042581"
---
# <a name="key-management-in-aspnet-core"></a>Управление ключами в ASP.NET Core

<a name="data-protection-implementation-key-management"></a>

Система защиты данных автоматически управляет временем существования главные ключи, используемые для защиты и снятие защиты полезных данных. Каждый раздел может существовать в одном из четырех этапов:

* Created — ключ существует в набора ключей, но еще не была активирована. Ключ не должен использоваться для новых операций защитить до истечения достаточно времени, ключ имели возможность распространять ко всем компьютерам, которые потребляют ресурсы этого набора ключей.

* Активен - ключ существует в набора ключей и должны использоваться для каждой новой операции защитить.

* Истек срок действия — ключ запуска существования естественным и больше не должен использоваться для новых операций защитить.

* Отменено - ключ скомпрометирован и не должны использоваться для новых операций защитить.

Ключи созданный active и истекшим сроком действия может использовать на снятие защиты полезных входящих данных. Отозванные ключи по умолчанию не может использоваться для снятие защиты полезных данных, но разработчик приложения может [переопределить это поведение](xref:security/data-protection/consumer-apis/dangerous-unprotect#data-protection-consumer-apis-dangerous-unprotect) при необходимости.

>[!WARNING]
> Разработчик может возникнуть желание удаления ключа из набора ключей (например, при удалении соответствующего файла из файловой системы). На этом этапе окончательно получить все данные, защищенные с помощью ключа, а не аварийного переопределение, как с помощью отозванных ключей. Удаление ключа является по-настоящему разрушающее поведение и поэтому система защиты данных предоставляет интерфейс API первого класса для выполнения данной операции.

## <a name="default-key-selection"></a>Выбор ключа по умолчанию

Когда система защиты данных считывает набора ключей из резервного хранилища, он попытается найти ключ «default» из набора ключей. Ключ по умолчанию используется для новых операций защитить.

Общие эвристический алгоритм является то, что система защиты данных выбирает ключ с самой последней даты активации как ключ по умолчанию. (Имеется небольшой настроечным разрешающее для часов между серверами неравномерного распределения). Если ключ просрочен или отозван, и если приложение не отключил автоматическое создание ключей, то будет создан новый ключ с немедленную активацию на [ключа истечение срока действия и последовательное](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management-expiration) политики ниже.

Причина система защиты данных немедленно создает новый ключ, а не откат к другой ключ является создание нового ключа, что следует обрабатывать как неявные срок действия всех ключей, которые были активированы до нового ключа. Общая идея заключается в новых ключей может быть настроен с помощью различных алгоритмов или механизмов шифрования при хранении, чем старые ключи, что система должна предпочтение откат текущей конфигурации.

Существует одно исключение. Если разработчик приложения [отключено автоматическое создание ключей](xref:security/data-protection/configuration/overview#disableautomatickeygeneration), то система защиты данных необходимо выбрать что-то в качестве ключа по умолчанию. В этом сценарии резервной системой будет выбран ключ не отозван с самой последней даты активации, с предпочтением в пользу ключи, у которых время для распространения на другие компьютеры в кластере. Система резервного использования может оказаться в результате выбора ключ с истекшим сроком действия по умолчанию. Система резервного использования никогда не выберет отозванных ключ как ключ по умолчанию, и если набора ключей пуст или был отозван каждый ключ система будет создавать ошибку при инициализации.

<a name="data-protection-implementation-key-management-expiration"></a>

## <a name="key-expiration-and-rolling"></a>Срок действия ключа и развертывания

При создании ключа, автоматически дала дату активации {now + 2 дня} и дату окончания срока действия {now + 90 дней}. Задержка 2 дня до активации дает ключевое время для распространения через систему. То есть он позволяет другим приложениям, указывает на хранилище для наблюдения за ключ в их следующий период автоматического обновления, что повышает вероятность того, что при ключ звонок может стать активной, ее распространения на все приложения, возможно, потребуется использовать его.

Если ключ по умолчанию истекает в течение двух дней и набора ключей еще нет ключом, который будет действовать после истечения срока действия ключа по умолчанию, система защиты данных автоматически сохранять новый ключ в связку ключей. Этот новый ключ имеет дату активации {ключ по умолчанию Дата истечения срока действия} и дату окончания срока действия {now + 90 дней}. Это позволяет системе автоматически изменять ключи на регулярной основе без перерывов в работе службы.

Могут возникнуть обстоятельства где создается ключ с немедленную активацию. Примером может служить, если приложение еще не выполняются в течение времени и истечет срок действия всех ключей в связку ключей. В этом случае ключ предоставляется дату активации {теперь} без задержки активации обычный 2 дня.

Время существования ключа по умолчанию составляет 90 дней, хотя это можно настроить, как показано в следующем примере.

```csharp
services.AddDataProtection()
       // use 14-day lifetime instead of 90-day lifetime
       .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
```

Администратор также может изменять всей системы по умолчанию, если явный вызов `SetDefaultKeyLifetime` переопределяет любую политику уровня системы. Время существования ключа по умолчанию не может быть менее 7 дней.

## <a name="automatic-key-ring-refresh"></a>Обновление автоматического набора ключей

При инициализации система защиты данных, он считывает из базового хранилища набора ключей и кэширует его в памяти. Этот кэш позволяет защитить и Unprotect операциям, без обращения резервного хранилища. Система автоматически проверит резервного хранилища для изменения, приблизительно каждые 24 часа или по истечении срока действия текущего ключа по умолчанию какое событие произойдет первым.

>[!WARNING]
> Разработчикам следует очень редко (если когда-нибудь) необходимо непосредственно использовать управление ключами API-интерфейсы. Система защиты данных выполнит автоматическое управление ключами, как описано выше.

Система защиты данных предоставляет интерфейс `IKeyManager` , можно использовать для проверки и внесения изменений для набора ключей. Система внедрения Зависимостей, предоставленный экземпляр `IDataProtectionProvider` также можно указать экземпляр `IKeyManager` за потребление ресурсов. Кроме того, можно извлечь `IKeyManager` прямо из `IServiceProvider` как в примере ниже.

Любая операция, которая изменяет набора ключей (Создание нового ключа явным образом или выполнении отзыв) сделает недействительными кэш в памяти. Следующий вызов `Protect` или `Unprotect` вызовет система защиты данных, повторное считывание набора ключей и повторное создание кэша.

В следующем примере показано использование `IKeyManager` интерфейса, изучать и манипулировать набора ключей, включая отзыв существующие ключи и создание нового ключа вручную.

[!code-csharp[](key-management/samples/key-management.cs)]

## <a name="key-storage"></a>Хранилища ключей

Система защиты данных имеет эвристики, при котором предпринимается попытка автоматически вывести расположение соответствующего хранилища ключей и механизм шифрования при хранении. Механизм сохранения ключа, также настраивается разработчиком приложения. Следующие документы обсудить встроенной реализации этих механизмов:

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>