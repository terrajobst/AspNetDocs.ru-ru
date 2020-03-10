---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: Создание строки подключения и работа с SQL Server LocalDB | Документация Майкрософт
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 20781ad760d3a0e4559ec4c7e18528f3686dcc02
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499014"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Создание строки подключения и работа с SQL Server LocalDB

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Создание строки подключения и работа с SQL Server LocalDB

Созданный класс `MovieDBContext` обрабатывает задачу подключения к базе данных и сопоставление объектов `Movie` с записями базы данных. Одним из вопросов, которые вы можете спросить, является указание того, к какой базе данных будет подключаться. На самом деле нет необходимости указывать, какую базу данных использовать, Entity Framework по умолчанию будет использовать [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb). В этом разделе мы явно добавим строку подключения в файл *Web. config* приложения.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) — это упрощенная версия SQL Server Express ядро СУБД, которая запускается по запросу и запускается в пользовательском режиме. LocalDB выполняется в специальном режиме выполнения SQL Server Express, который позволяет работать с базами данных в виде *MDF* -файлов. Как правило, файлы базы данных LocalDB хранятся в папке *приложения\_данных* веб-проекта.

SQL Server Express не рекомендуется использовать в рабочих веб-приложениях. LocalDB в частности не следует использовать для рабочей среды с веб-приложением, поскольку оно не предназначено для работы с IIS. Однако базу данных LocalDB можно легко перенести в SQL Server или SQL Azure.

В Visual Studio 2017 LocalDB устанавливается по умолчанию в Visual Studio.

По умолчанию Entity Framework ищет строку подключения с именем, аналогичную классу контекста объекта (`MovieDBContext` для этого проекта). Дополнительные сведения см. в разделе [SQL Server строки подключения для веб-приложений ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx).

Откройте корневой файл *Web. config* приложения, показанный ниже. (Не файл *Web. config* в папке *views* .)

![](creating-a-connection-string/_static/image1.png)

Найдите элемент `<connectionStrings>`:

![](creating-a-connection-string/_static/image2.png)

Добавьте следующую строку подключения в элемент `<connectionStrings>` в файле *Web. config* .

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

В следующем примере показана часть файла *Web. config* с добавленной новой строкой подключения:

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

Две строки подключения очень похожи. Первая строка подключения называется `DefaultConnection` и используется для базы данных членства для управления доступом к приложению. Добавленная строка подключения указывает базу данных LocalDB с именем *Movie. mdf* , расположенную в папке *приложения\_данных* . Мы не будем использовать базу данных членства в этом руководстве. Дополнительные сведения о членстве, проверке подлинности и безопасности см. в моем руководстве [Создание приложения ASP.NET MVC с проверкой подлинности и базой данных SQL и развертывание в службе приложений Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).

Имя строки подключения должно совпадать с именем класса [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) .

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

В действительности не нужно добавлять строку подключения `MovieDBContext`. Если строка подключения не указана, Entity Framework создаст базу данных LocalDB в каталоге Users с полным именем класса [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) (в данном случае `MvcMovie.Models.MovieDBContext`). Вы можете присвоить базе данных любое имя, если оно имеет значение *. Суффикс MDF* . Например, можно присвоить имя базе данных *мифилмс. mdf*.

Далее предстоит создать новый класс `MoviesController`, который можно использовать для отображения данных фильмов и предоставления пользователям возможности создавать новые списки фильмов.

> [!div class="step-by-step"]
> [Назад](adding-a-model.md)
> [Вперед](accessing-your-models-data-from-a-controller.md)
