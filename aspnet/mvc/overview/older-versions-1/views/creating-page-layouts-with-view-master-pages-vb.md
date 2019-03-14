---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: Создание макетов страниц с главными страницами представлений (Visual Basic) | Документация Майкрософт
author: microsoft
description: В этом руководстве вы узнаете, как создать общий макет страницы для нескольких страниц в приложении, используя преимущества представления главных страниц. Можно использовать...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 4ff74b1dc1d83b7ec1c8ecf6eca341a5cd14403f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026831"
---
<a name="creating-page-layouts-with-view-master-pages-vb"></a>Создание макетов страниц с эталонными страницами представлений (VB)
====================
по [Microsoft](https://github.com/microsoft)

[Загрузить PDF-файл](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> В этом руководстве вы узнаете, как создать общий макет страницы для нескольких страниц в приложении, используя преимущества представления главных страниц. Например, главной страницы представления, можно использовать для определения макета страницы с двумя столбцами и используется режим двух столбцов для всех страниц в веб-приложении.


## <a name="creating-page-layouts-with-view-master-pages"></a>Создание макетов страниц с главными страницами представлений

В этом руководстве вы узнаете, как создать общий макет страницы для нескольких страниц в приложении, используя преимущества представления главных страниц. Например, главной страницы представления, можно использовать для определения макета страницы с двумя столбцами и используется режим двух столбцов для всех страниц в веб-приложении.

Вы также можно воспользоваться преимуществами представления главных страниц для совместного использования типичного содержимого на несколько страниц в приложении. Например можно поместить Эмблема веб-сайта, ссылки навигации и рекламных объявлений на главной странице представления. Таким образом, каждой страницы в приложении будет автоматически отображаться это содержимое.

В этом руководстве вы узнаете, как создать новую главную страницу и создать новую страницу содержимого представления, основанные на главной странице.

### <a name="creating-a-view-master-page"></a>Создание представления главной страницы

Начнем с создания представления главной страницы, определяющий двухколонной разметке. Добавляемый новой главной страницы представления проекта MVC, щелкнув правой кнопкой мыши папку Views\Shared, выбрав вариант меню **добавить, новый элемент**и выбрав шаблон MVC представления главной страницы (см. рис. 1).


[![Добавление представления главной страницы](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**Рис 01**: Добавление представления главной страницы ([Просмотр полноразмерного изображения](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))


В приложении можно создать более одной главной страницы представления. Каждый пакет главных страниц представления можно задать макет в другую страницу. Например может потребоваться определенные страницы, чтобы двухколонной разметке и другие страницы, чтобы макет с тремя столбцами.

Главная страница представления выглядит очень похожим стандартного представления ASP.NET MVC. Тем не менее, в отличие от обычного представления главной страницы представления содержит один или несколько `<asp:ContentPlaceHolder>` теги. `<contentplaceholder>` Теги используются для пометки части главной страницы, можно переопределить в отдельных страниц содержимого.

Например главной страницы представления в листинге 1 определяет двухколонной разметке. Он содержит два `<contentplaceholder>` теги. Один `<ContentPlaceHolder>` для каждого столбца.

**Листинг 1. `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

Тело главной страницы в листинге 1 содержит два представления `<div>` теги, которые соответствуют двух столбцов. Класс каскадных таблиц стилей столбцов применяется к обоим `<div>` теги. Этот класс определен в таблице стилей, объявленные в верхней части главной страницы. Можно просмотреть просмотру главной страницы представления с переключением в режим конструктора. Перейдите на вкладку "Конструктор" в левом нижнем углу редактора исходного кода (см. рис. 2).


[![Предварительный просмотр главной страницы в конструкторе](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**Рис. 02**: Предварительный просмотр главной страницы в конструкторе ([Просмотр полноразмерного изображения](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))


### <a name="creating-a-view-content-page"></a>Создание представления содержимого страницы

После создания представления главной страницы, можно создать один или несколько представление страницы содержимого на основе главной страницы представления. Например, можно создать страницу содержимого представления индекса для контроллера Home щелкните правой кнопкой мыши папку Views\Home, выбрав **добавить, новый элемент**, выбрав **страница содержимого представления MVC** шаблон, введя имя Index.aspx и выберите команду добавить кнопки мыши (см. рис. 3).


[![Добавление представления содержимого страницы](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**Рис 03**: Добавление страницы содержимого представления ([Просмотр полноразмерного изображения](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))


После нажатия кнопки «Добавить», новое диалоговое окно появляется, дающий возможность выбора представления главной страницы должен быть сопоставлен страница содержимого представления (см. рис. 4). Можно перейти на главную страницу Site.master представления, созданную в предыдущем разделе.


[![Выбор главной страницы](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**Рис. 04**: Выбор главной страницы ([Просмотр полноразмерного изображения](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))


Создав новую страницу содержимого представления, на основе на главной странице Site.master, вы получите файл в листинге 2.

**Листинг 2. `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

Обратите внимание, что это представление содержит `<asp:Content>` тег, соответствующий каждому `<asp:ContentPlaceHolder>` тегов в главной страницы представления. Каждый `<asp:Content>` тег содержит атрибут ContentPlaceHolderID, который указывает на конкретный `<asp:ContentPlaceHolder>` , оно переопределяет.

Кроме того, обратите внимание, что странице представления содержимого в листинге 2 не содержит обычный открывающий и закрывающий HTML-теги. Например, он не содержит открывающим и закрывающим `<html>` или `<head>` теги. Все обычные открывающие и закрывающие теги содержатся в главной страницы представления.

Любое содержимое, которое будет отображаться на странице содержимого представления должен быть помещен в `<asp:Content>` тега. Если поместить любой код HTML или другое содержимое за пределами этих тегов, будут получать ошибку при попытке просмотра страницы.

Не требуется переопределять каждый `<asp:ContentPlaceHolder>` тег из главной страницы в представлении содержимого страницы. Необходимо переопределить `<asp:ContentPlaceHolder>` тег, если вы хотите заменить это конкретное содержимое тега.

Например, измененный представление Index в листинге 3 содержит только два `<asp:Content>` теги. Каждый из `<asp:Content>` теги включает какой-нибудь текст.

**Листинг 3. `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

При запросе представления в листинге 3, он осуществляет отрисовку страницы на рис. 5. Обратите внимание на то, что представление отображает страницу с двумя столбцами. Кроме того, обратите внимание, что содержимое на странице содержимого объединяется с содержимым из главной страницы представления.


[![Страница содержимого представления индекса](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**05 рис**: Страница содержимого представления индекса ([Просмотр полноразмерного изображения](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))


### <a name="modifying-view-master-page-content"></a>Изменение содержимого образец страницы

Одна из проблем возникают почти сразу же в том случае, при работе с главными страницами представления — это задача Изменение представления содержимого главной страницы, при запросе страницы содержимого в другое представление. Например требуется каждой страницы в веб-приложения к уникальным заголовком. Тем не менее заголовка объявлен на главной странице представления и не в представлении содержимого страницы. Таким образом как настроить заголовок страницы для каждой страницы содержимого представления?

Существует два способа, которые можно изменить заголовок, отображаемый с содержимым страницы представления. Во-первых, можно назначить заголовком для атрибута title `<%@ page %>` объявление директивы в верхней части страницы содержимого представления. Например если вы хотите назначить заголовок страницы «Отлично Super веб-сайт» в представление Index, можно включить следующую директиву в верхней части представления индекса:

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

При подготовке к просмотру в представление Index в браузер, требуемый заголовок отображается в заголовке окна браузера:


[![Строка заголовка браузера](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)


Есть одно важное требование, главной страницы представления должна удовлетворять в порядке для атрибута title, для работы. Главная страница представления должен содержать `<head runat="server">` тег вместо обычной `<head>` тег для заголовка. Если `<head>` тег не поддерживает runat = «server» атрибута, то заголовок не будет отображаться. Представление по умолчанию, главной страницы содержит обязательные `<head runat="server">` тега.

Альтернативный подход к изменению содержимого главной страницы на странице содержимого отдельного представления является включение регион, который нужно внести изменения в `<asp:ContentPlaceHolder>` тега. Например представьте, что вы хотите изменить не только название, но теги meta, преобразовываемый для главной страницы представления. Главной страницы представления в листинге 4 содержит `<asp:ContentPlaceHolder>` тег в его `<head>` тега.

**Листинг 4. `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

Обратите внимание, что `<asp:ContentPlaceHolder>` тег в листинге 4 включает содержимое по умолчанию: по умолчанию заголовок и теги метаданных по умолчанию. Если не переопределить это `<asp:ContentPlaceHolder>` тег на странице отдельного представления содержимого, то отображается содержимое по умолчанию.

Страница содержимого представления в листинге 5 переопределяет `<asp:ContentPlaceHolder>` тег, чтобы отобразить пользовательский заголовок и настраиваемые теги метаданных.

**Листинг 5. `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>Сводка

Это руководство предоставляет вам основные сведения о можно просмотреть главных страниц и страниц содержимого. Вы узнали, как создать новое представление главные страницы и создавать представления содержимого страницы, на их основе. Мы также рассмотрели, как изменять содержимое главной страницы представления из страницы содержания конкретное представление.

> [!div class="step-by-step"]
> [Назад](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [Вперед](passing-data-to-view-master-pages-vb.md)