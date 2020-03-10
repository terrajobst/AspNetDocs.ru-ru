---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Добавление модели | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: c5525cfe940cadff5113c63eb0508d15697b5606
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499086"
---
# <a name="adding-a-model"></a>Добавление модели

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

В этом разделе вы добавите некоторые классы для управления фильмами в базе данных. Эти классы будут &quot;моделью&quot; части приложения ASP.NET MVC.

Вы будете использовать .NET Frameworkную технологию доступа к данным, известную как [Entity Framework](https://docs.microsoft.com/ef/) , для определения и работы с этими классами модели. Entity Framework (часто называемый EF) поддерживает парадигму разработки, именуемую *Code First*. Code First позволяет создавать объекты модели, создавая простые классы. (Они также называются классами POCO, от &quot;обычных объектов CLR.&quot;) Затем базу данных можно создать в режиме реального времени из классов, что позволяет выполнять очень четкий и быстрый рабочий процесс разработки. Если сначала необходимо создать базу данных, вы по-прежнему можете следовать этому учебнику, чтобы узнать о разработке приложений MVC и EF. Затем вы можете следовать учебнику по созданию шаблонов для Tom Физмакенс [ASP.NET](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) , в котором рассматривается первый подход к базе данных.

## <a name="adding-model-classes"></a>Добавление классов модели

В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.

![](adding-a-model/_static/image1.png)

Введите имя *класса* &quot;&quot;фильмов.

Добавьте в класс `Movie` следующие пять свойств:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Мы будем использовать класс `Movie` для представления фильмов в базе данных. Каждый экземпляр объекта `Movie` будет соответствовать строке в таблице базы данных, а каждое свойство класса `Movie` будет сопоставляться со столбцом в таблице.

Примечание. для использования System. Data. Entity и связанного класса необходимо установить [Entity Framework пакет NuGet](https://www.nuget.org/packages/EntityFramework/). Чтобы получить дополнительные инструкции, перейдите по ссылке.

В том же файле добавьте следующий класс `MovieDBContext`:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

Класс `MovieDBContext` представляет контекст базы данных Entity Framework Movie, который обрабатывает выборку, хранение и обновление экземпляров класса `Movie` в базе данных. `MovieDBContext` является производным от базового класса `DbContext`, предоставляемого Entity Framework.

Чтобы иметь возможность ссылаться на `DbContext` и `DbSet`, необходимо добавить в начало файла следующую инструкцию `using`:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Это можно сделать, вручную добавив оператор using или наведя указатель мыши на красную волнистую линию, щелкнуть `Show potential fixes` и выбрать `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

Примечание. несколько неиспользуемых инструкций `using` были удалены. В Visual Studio неиспользуемые зависимости будут отображаться серым цветом. Вы можете удалить неиспользуемые зависимости, наведя указатель мыши на серые зависимости, щелкните `Show potential fixes` и выберите **Удалить неиспользуемые команды using.**

![](adding-a-model/_static/image3.png)

Мы наконец добавили модель (M в MVC). В следующем разделе вы будете работать со строкой подключения к базе данных.

> [!div class="step-by-step"]
> [Назад](adding-a-view.md)
> [Вперед](creating-a-connection-string.md)
