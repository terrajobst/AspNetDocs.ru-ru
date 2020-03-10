---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: Обновление приложения ASP.NET MVC 1,0 до ASP.NET MVC 2 | Документация Майкрософт
author: rick-anderson
description: В этом документе описано, как выполнить обновление вручную и с помощью мастера ASP.NET MVC 1,0 для ASP.NET MVC 2. Этот документ также доступен для d...
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517302"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a>Обновление приложения ASP.NET MVC 1.0 до ASP.NET MVC 2

> В этом документе описано, как выполнить обновление вручную и с помощью мастера ASP.NET MVC 1,0 для ASP.NET MVC 2. Этот документ также доступен для [загрузки](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)

## <a name="introduction"></a>Введение

ASP.NET MVC 2 можно установить параллельно с ASP.NET MVC 1,0 на том же сервере. Это позволяет разработчикам приложений гибко выбирать время обновления приложения ASP.NET MVC 1,0 до ASP.NET MVC 2.

В состав Visual Studio 2010 входит мастер, который обновляет существующие проекты ASP.NET MVC 1,0, созданные с помощью Visual Studio 2008, до ASP.NET MVC 2. Мастер обновления запускается путем открытия проекта ASP.NET MVC 1,0 в Visual Studio 2010.

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a>Мастер обновления для ASP.NET MVC 1,0 в Visual Studio 2008 SP1

Чтобы обновить приложение ASP.NET MVC 1,0 до ASP.NET MVC 2 в Visual Studio 2008 с пакетом обновления 1 (SP1), используйте приложение (не поддерживается) Мвкаппконвертер. Это приложение можно скачать по следующему URL-адресу:

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a>Обновление проекта ASP.NET MVC 1,0 вручную

Чтобы вручную обновить существующее приложение ASP.NET MVC 1,0 до версии 2, выполните следующие действия.

1. Создайте резервную копию существующего проекта.
2. В текстовом редакторе откройте файл проекта (файл с расширением CSPROJ или VBPROJ) и найдите элемент Прожекттипегуид. В качестве значения этого элемента замените GUID {603c0e0b-db56-11dc-be95-000d561079b0} на {F85E285D-A4E0-4152-9332-AB1D724D3325}. По завершении значение этого элемента должно быть следующим: 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. В корневой папке веб-приложения измените файл Web. config. Выполните поиск System. Web. MVC, Version = 1.0.0.0 и замените все экземпляры на System. Web. MVC, Version = 2.0.0.0.
4. Повторите предыдущий шаг для файла Web. config, расположенного в папке Views.
5. Откройте проект с помощью Visual Studio, а затем в **Обозреватель решений**разверните узел **ссылки** . Удалите ссылку на System. Web. MVC (которая указывает на сборку версии 1,0). Добавьте ссылку на System. Web. MVC (v 2.0.0.0).
6. Добавьте следующий элемент bindingRedirect в файл Web. config в корне приложения в разделе конфигурации:   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. Создайте пустое приложение ASP.NET MVC 2. Скопируйте файлы из папки Scripts нового приложения в папку Scripts существующего приложения.
8. Обновите существующий CSS-файл приложения €™ s с определениями стиля CSS в файле Site. CSS.
9. Скомпилируйте приложение и запустите его. Если возникнут какие-либо ошибки, см. раздел критические изменения на странице [новые возможности ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) .
