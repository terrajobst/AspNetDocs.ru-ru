---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: Добавление модели | Документация Майкрософт
author: Rick-Anderson
description: Примечание. Обновленная версия этого учебника доступна здесь, в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще в исполнении и демонстрации...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434418"
---
# <a name="adding-a-model"></a>Добавление модели

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > Обновленная версия этого учебника доступна [здесь](../../getting-started/introduction/getting-started.md) , в которой используется ASP.NET MVC 5 и Visual Studio 2013. Он более безопасен, гораздо проще следовать и демонстрирует дополнительные функции.

В этом разделе вы добавите некоторые классы для управления фильмами в базе данных. Эти классы будут &quot;моделью,&quot; частью приложения MVC ASP.NET.

Вы будете использовать .NET Frameworkную технологию доступа к данным, известную как [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) , для определения и работы с этими классами модели. Entity Framework (часто называемый EF) поддерживает парадигму разработки, именуемую *Code First*. Code First позволяет создавать объекты модели, создавая простые классы. (Они также называются классами POCO, от &quot;обычных объектов CLR.&quot;) Затем базу данных можно создать в режиме реального времени из классов, что позволяет выполнять очень четкий и быстрый рабочий процесс разработки.

## <a name="adding-model-classes"></a>Добавление классов модели

В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.

![](adding-a-model/_static/image1.png)

Введите имя *класса* &quot;&quot;фильмов.

Добавьте в класс `Movie` следующие пять свойств:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

Мы будем использовать класс `Movie` для представления фильмов в базе данных. Каждый экземпляр объекта `Movie` будет соответствовать строке в таблице базы данных, а каждое свойство класса `Movie` будет сопоставляться со столбцом в таблице.

В том же файле добавьте следующий класс `MovieDBContext`:

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

Класс `MovieDBContext` представляет контекст базы данных Entity Framework Movie, который обрабатывает выборку, хранение и обновление экземпляров класса `Movie` в базе данных. `MovieDBContext` является производным от базового класса `DbContext`, предоставляемого Entity Framework.

Чтобы иметь возможность ссылаться на `DbContext` и `DbSet`, необходимо добавить в начало файла следующую инструкцию `using`:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Полный файл *Movie.CS* показан ниже. (Несколько ненужных инструкций using были удалены.)

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Создание строки подключения и работа с SQL Server LocalDB

Созданный класс `MovieDBContext` обрабатывает задачу подключения к базе данных и сопоставление объектов `Movie` с записями базы данных. Одним из вопросов, которые вы можете спросить, является указание того, к какой базе данных будет подключаться. Это можно сделать, добавив сведения о подключении в файл *Web. config* приложения.

Откройте корневой файл *Web. config* приложения. (Не файл *Web. config* в папке *views* .) Откройте файл *Web. config* , выделенный красным цветом.

![](adding-a-model/_static/image2.png)

Добавьте следующую строку подключения в элемент `<connectionStrings>` в файле *Web. config* .

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

В следующем примере показана часть файла *Web. config* с добавленной новой строкой подключения:

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

Небольшой объем кода и XML — это все, что необходимо для написания, чтобы представить и сохранить данные фильмов в базе данных.

Далее предстоит создать новый класс `MoviesController`, который можно использовать для отображения данных фильмов и предоставления пользователям возможности создавать новые списки фильмов.

> [!div class="step-by-step"]
> [Назад](adding-a-view.md)
> [Вперед](accessing-your-models-data-from-a-controller.md)
