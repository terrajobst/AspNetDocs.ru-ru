---
uid: mobile/device-simulators
title: Имитация популярных мобильных устройств для тестирования с помощью ASP.NET | Документация Майкрософт
author: rick-anderson
description: Скачайте эмуляторы для популярных мобильных устройств и браузеров для тестирования с помощью приложения ASP.NET. Включает в себя iPhone, Android, BrowserStack и многое другое.
ms.author: riande
ms.date: 10/11/2018
ms.custom: seoapril2019
ms.assetid: bfb5612e-c3ec-4f28-b43b-63d781aa2272
msc.legacyurl: /mobile/device-simulators
msc.type: content
ms.openlocfilehash: aec442e05a7db69dfaea4b0cca53bbf41792500c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59412155"
---
# <a name="simulate-popular-mobile-devices-for-testing"></a>Имитация популярных мобильных устройств для тестирования

> Эмуляторы для популярных мобильных устройств и браузеров можно загрузить по следующим ссылкам.

| Устройство или браузер | Эмулятор или симулятор |
| --- | --- |
| BrowserStack размещенных виртуализации браузера ![BrowserStack размещенных виртуализации браузера](device-simulators/_static/image1.png) | [Виртуализация браузера BrowserStack](http://browserstack.com) тестирование локальной или рабочей среды в любом браузере на любой платформе. Можно создать туннель между вашей машине, а также сети BrowserStack собственные размещенной виртуальной машине. Убедитесь, что для получения [расширение Visual Studio BrowserStack](https://marketplace.visualstudio.com/items?itemName=browserstackcom.BrowserStack) для еще более эффективной. |
| iPhone / iPod / iPad | [Электрический Mobile Studio](http://www.electricplum.com/studio.aspx) iPhone и iPad симуляторы для Windows, а также адаптивный разработать инструмент. |
| Android | [Android Studio](https://developer.android.com/studio/) или [Visual Studio Emulator для Android](https://visualstudio.microsoft.com/vs/msft-android-emulator/) |
| Opera Mobile | [Классический эмулятор Opera Mobile](https://www.opera.com/developer/mobile-emulator) |
| Windows Mobile 6.5.3 | [Набор средств разработчика Windows Mobile 6.5.3](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=c0213f68-2e01-4e5c-a8b2-35e081dcf1ca&amp;displaylang=en) Обратите внимание, что для предоставления доступа к сети телефона, необходимо также включены в VPC сетевого адаптера [Virtual PC 2007](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=04d26402-3199-48a3-afa2-2dc0b40a73b6&amp;DisplayLang=en). Для подключения IE на телефоне, чтобы сервер разработки Visual Studio, см. в разделе [Kiran Патил записи блога](http://kiranpatils.wordpress.com/2009/11/19/access-internetlocal-website-from-your-windows-mobile-device-emulators/). |

> [!NOTE]
> Если вы хотите просмотреть приложения на настоящем мобильном устройстве (который является единственным параметром для полного тестирования iPhone или iPad, так как не true эмулятора для Windows) необходимо разместить приложение в IIS или IIS Express. Нельзя использовать легко встроенные веб-сервер Visual Studio, так как он не будет отвечать на запросы с других компьютеров.
