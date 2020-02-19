---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
title: Улучшение методов Details и Delete (VB) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1)...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: c5c14ef0-c128-4dc1-8c01-7f0fdb09e411
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 08d80cac071907e927bb30df53c6f84a28f53156
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456261"
---
# <a name="improving-the-details-and-delete-methods-vb"></a>Изучение методов Details и Delete (VB)

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете об основах создания веб-приложения ASP.NET MVC с помощью Microsoft Visual Web Developer 2010 Express с пакетом обновления 1 (SP1), который является бесплатной версией Microsoft Visual Studio. Прежде чем начать, убедитесь, что установлены предварительные требования, перечисленные ниже. Чтобы установить все эти компоненты, щелкните следующую ссылку: [установщик веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Кроме того, вы можете отдельно установить необходимые компоненты, используя следующие ссылки:
> 
> - [Предварительные требования для Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Обновление инструментов ASP.NET MVC 3](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(поддержка времени выполнения и средств)
> 
> Если вы используете Visual Studio 2010 вместо Visual Web Developer 2010, установите необходимые компоненты, щелкнув следующую ссылку: [Предварительные требования для Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Для этого раздела доступен проект Visual Web Developer с исходным кодом VB.NET. [Скачайте версию VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). При желании C#переключитесь на [ C# версию](../cs/improving-the-details-and-delete-methods.md) этого учебника.

В этой части руководства вы вносите некоторые улучшения в автоматически создаваемые `Details` и `Delete` методы. Эти изменения не являются обязательными, но с помощью всего нескольких небольших фрагментов кода можно легко улучшить приложение.

## <a name="improving-the-details-and-delete-methods"></a>Улучшение методов Details и DELETE

При формировании шаблона контроллера `Movie` ASP.NET код MVC, который работает великолепно, но его можно сделать более надежным с помощью всего лишь нескольких небольших изменений.

Откройте контроллер `Movie` и измените метод `Details`, вернувшись `HttpNotFound`, если фильм не найден. Также следует изменить метод `Details`, чтобы задать значение по умолчанию для идентификатора, который передается ему. (В [части 6](examining-the-edit-methods-and-edit-view.md) этого руководства вы внесли аналогичные изменения в метод `Edit`.) Однако необходимо изменить тип возвращаемого значения метода `Details` с `ViewResult` на `ActionResult`, так как метод `HttpNotFound` не возвращает объект `ViewResult`. В следующем примере показан измененный метод `Details`.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample1.vb)]

Code First упрощает поиск данных с помощью метода `Find`. Важная функция безопасности, встроенная в метод, заключается в том, что код проверяет, был ли метод `Find` нашел фильм, прежде чем код пытается выполнить с ним какое-либо действие. Например, злоумышленник может вызвать ошибки на сайте, изменив URL-адрес, созданный ссылками, с `http://localhost:xxxx/Movies/Details/1` на нечто вроде `http://localhost:xxxx/Movies/Details/12345` (или какое-либо другое значение, не представляющее реальный фильм). Если вы не проверите наличие пустого фильма, это может привести к ошибке базы данных.

Аналогичным образом измените методы `Delete` и `DeleteConfirmed`, чтобы указать значение по умолчанию для параметра ID и вернуть `HttpNotFound`, если фильм не найден. Обновленные методы `Delete` в контроллере `Movie` показаны ниже.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample2.vb)]

Обратите внимание, что метод `Delete` не удаляет данные. Выполнение операции удаления в ответ на запрос GET (или выполнение операции редактирования, создания или любой другой операции, изменяющей данные) открывает брешь в системе безопасности. Дополнительные сведения об этом см. в разделе блога Вальтер для Стивен [ASP.NET #46 — не используйте ссылки DELETE, так как они создают бреши в системе безопасности](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

Метод `HttpPost`, который удаляет данные, называется `DeleteConfirmed`, поэтому метод HTTP POST обладает уникальной сигнатурой или именем. Ниже приведены сигнатуры двух методов:

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample3.vb)]

Среда CLR требует наличия перегруженных методов, чтобы иметь уникальную сигнатуру (то же самое имя, другой список параметров). Однако здесь необходимы два метода удаления — один для GET и один для последующей, так что оба требуют одинаковой сигнатуры. (Они оба должны принимать целочисленное значение в качестве параметра.)

Чтобы отсортировать это, можно выполнить несколько действий. Одним из них является присвоение методам различных имен. Мы сделали это в предыдущем примере. Однако в этом случае возникает небольшая проблема: ASP.NET сопоставляет сегменты URL-адреса с методами действий по имени, а при переименовании метода, как правило, маршрутизация не сможет найти этот метод. Решение показано в примере, а именно: в метод `ActionName("Delete")` следует добавить атрибут `DeleteConfirmed`. Это эффективно выполняет сопоставление для системы маршрутизации, чтобы URL-адрес, включающий <em>/делете/</em>для запроса POST, нашел метод `DeleteConfirmed`.

Другой способ избежать проблем с методами, имеющими идентичные имена и сигнатуры, — искусственно изменить сигнатуру метода POST, включив в него неиспользуемый параметр. Например, некоторые разработчики добавляют тип параметра `FormCollection`, который передается методу POST, а затем просто не использует параметр:

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample4.vb)]

## <a name="wrapping-up"></a>Заключение

Теперь у вас есть законченное приложение MVC ASP.NET, которое хранит данные в базе данных SQL Server Compact. Вы можете создавать, читать, обновлять, удалять и искать фильмы.

![](improving-the-details-and-delete-methods/_static/image1.png)

В этом учебном курсе было начато создание контроллеров, связывание их с представлениями и передача жестко запрограммированных данных. Затем вы создали и разработали модель данных. Entity Framework Code First создали базу данных из модели данных на лету, и система формирования шаблонов MVC ASP.NET автоматически создала методы и представления действий для базовых операций CRUD. Затем вы добавили форму поиска, которая позволяет пользователям выполнять поиск в базе данных. Вы изменили базу данных, включив в нее новый столбец данных, а затем обновили две страницы для создания и вывода новых данных. Вы добавили проверку, пометив модель данных атрибутами из пространства имен `DataAnnotations`. Результирующая проверка выполняется на стороне клиента и на сервере.

Если вы хотите развернуть приложение, полезно сначала протестировать приложение на локальном сервере IIS 7. Эту ссылку для [установщика веб-платформы](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;) можно использовать для включения параметра IIS для приложений ASP.NET. См. следующие ссылки на развертывание:

- [Схема содержимого развертывания ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx)
- [Включение IIS 7. x](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [Развертывание проектов веб-приложений](https://msdn.microsoft.com/library/dd394698.aspx)

Теперь я рекомендую перейти на наш промежуточный уровень [создания модели данных Entity Framework для приложения ASP.NET MVC](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) и руководств по [музыкальному хранилищу MVC](../../mvc-music-store/mvc-music-store-part-1.md) , ИЗУЧИТЬ [статьи ASP.NET в MSDN](https://msdn.microsoft.com/library/gg416514(VS.98).aspx), а также ознакомиться со многими видео и ресурсами на [https://asp.net/mvc](https://asp.net/mvc) , чтобы больше узнать о ASP.NET MVC! [Форумы ASP.NET MVC](https://forums.asp.net/1146.aspx) — это отличное место для задаваемых вопросов.

Вот и все!

— Скотт Hanselman ([http://hanselman.com](http://hanselman.com) и [@shanselman](http://twitter.com/shanselman) в Twitter) и Рик Андерсон ( [blogs.MSDN.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [Назад](adding-validation-to-the-model.md)
