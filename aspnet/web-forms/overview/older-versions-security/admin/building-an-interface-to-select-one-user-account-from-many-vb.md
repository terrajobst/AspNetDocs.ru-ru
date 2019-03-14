---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: Создание интерфейса для выбора одной учетной записи пользователя из многих (VB) | Документация Майкрософт
author: rick-anderson
description: В этом руководстве мы построим пользовательский интерфейс с сеткой разбитого на страницы, фильтруемое. В частности пользовательского интерфейса будет состоять из ряда элементов управления LinkButton для...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: bb30c5d3ce6e04f60d8192e8ed0404b89031b4b9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038581"
---
<a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>Создание интерфейса для выбора одной учетной записи пользователя из многих (VB)
====================
по [Скотт Митчелл](https://twitter.com/ScottOnWriting)

[Скачать код](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) или [скачать PDF](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> В этом руководстве мы построим пользовательский интерфейс с сеткой разбитого на страницы, фильтруемое. В частности пользовательского интерфейса будет состоять из ряда элементов управления LinkButton для фильтрации результатов на основе начальной буквы имени пользователя и элемента управления GridView для отображения соответствующих пользователей. Мы начнем, перечисляя все учетные записи пользователя в элементе управления GridView. Затем на шаге 3, мы добавим фильтр элементов управления LinkButton. Шаг 4 рассматривает разбиение по страницам отфильтрованные результаты. Интерфейс, созданный на шагах 2 – 4 будет использоваться в последующих руководствах для выполнения административных задач для учетной записи пользователя.


## <a name="introduction"></a>Вступление

В <a id="_msoanchor_1"> </a> [ *назначение ролей пользователям* ](../roles/assigning-roles-to-users-vb.md) мы создали элементарные интерфейс администратор может выбрать пользователя и управление ей ролями. В частности интерфейс предоставлен администратору стрелку раскрывающегося списка всех пользователей. Такой интерфейс подходит в том случае, если присутствуют, но десяток пользователь учетные записи, но неудобным для сайтов, сотни или тысячи учетных записей. Разбитого на страницы, фильтруемое сетки — более подходящий пользовательский интерфейс для веб-сайтов с большим числом пользователей базовыми классами.

В этом руководстве мы построим такой пользовательский интерфейс. В частности пользовательского интерфейса будет состоять из ряда элементов управления LinkButton для фильтрации результатов на основе начальной буквы имени пользователя и элемента управления GridView для отображения соответствующих пользователей. Мы начнем, перечисляя все учетные записи пользователя в элементе управления GridView. Затем на шаге 3, мы добавим фильтр элементов управления LinkButton. Шаг 4 рассматривает разбиение по страницам отфильтрованные результаты. Интерфейс, созданный на шагах 2 – 4 будет использоваться в последующих руководствах для выполнения административных задач для учетной записи пользователя.

Давайте начнем!

## <a name="step-1-adding-new-aspnet-pages"></a>Шаг 1. Добавление новых страниц ASP.NET

В этом руководстве и следующих двух мы остановимся подробнее различных функций для работы с веб-администрирования и возможности. Нам понадобится несколько страниц ASP.NET для реализации в разделах, проверены в данных учебных курсах. Давайте создавать эти страницы и обновите карту узла.

Начнем с создания новой папки в проект с именем `Administration`. Добавьте два новых страниц ASP.NET к папке, связывание каждой страницы с `Site.master` главной страницы. Имя страницы:

- `ManageUsers.aspx`
- `UserInformation.aspx`

Также добавьте две страницы корневой каталог веб сайта: `ChangePassword.aspx` и `RecoverPassword.aspx`.

Эти четыре страницы на этом этапе требуется два содержимого элемента управления: один для каждого из элементов управления ContentPlaceHolder на главной странице: `MainContent` и `LoginContent`.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

Мы хотим Показать разметки главной страницы по умолчанию для `LoginContent` ContentPlaceHolder для этих страниц. Таким образом, удалить декларативная разметка для `Content2` содержимого элемента управления. После этого разметка страницы должен содержать только один элемент управления содержимым.

Страницы ASP.NET в `Administration` папку предназначены исключительно для пользователей с правами администратора. Мы добавили роли "Администраторы" в систему в <a id="_msoanchor_2"> </a> [ *Создание и управление ролями* ](../roles/creating-and-managing-roles-vb.md) руководства, ограничить доступ к этим двум страницам, к этой роли. Для этого добавьте `Web.config` файл `Administration` папки и настроить его `<authorization>` элемент должен признать, пользователи в роли "Администраторы" и запретив все остальные.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

На этом этапе проекта обозреватель решений должен выглядеть снимок экрана, показанный на рис. 1.


[![На веб-сайт были добавлены четыре новые страницы и файл Web.config](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**Рис. 1**: Четыре новых страниц и `Web.config` файла были добавлены на веб-сайт ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png))


Наконец, обновите карту узла (`Web.sitemap`) для включения записи для `ManageUsers.aspx` страницы. Добавьте следующий код XML после `<siteMapNode>` мы добавили учебников ролей.

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

С помощью карты узла обновлен посетите сайт через браузер. Как показано на рис. 2, навигации в левой части теперь включает элементы для администрирования учебники.


[![Карты узла имеется узел под названием Администрирование пользователей](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**Рис. 2**: Администрирование пользователей узел под названием включает в себя карты узла ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png))


## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>Шаг 2. Получение списка всех учетных записей пользователя в элементе управления GridView

Наша конечная цель для этого учебника является для создания разбитого на страницы, фильтруемое сетки с помощью которого администратор может выбрать учетную запись пользователя для управления. Давайте начнем с листинг *все* пользователей в элементе управления GridView. После завершения этого, мы добавим, фильтрации и разбиения на страницы интерфейсы и функциональные возможности.

Откройте `ManageUsers.aspx` странице в `Administration` папку и добавьте элемент управления GridView, установив его `ID` для `UserAccounts` чуть позже, мы напишем код для привязки к GridView с помощью набора учетных записей пользователей `Membership` класса `GetAllUsers` метод. Как уже говорилось в предыдущих учебных курсах, `GetAllUsers` возвращает `MembershipUserCollection` объект, который представляет собой коллекцию из `MembershipUser` объектов. Каждый `MembershipUser` в коллекции включает в себя свойства, такие как `UserName`, `Email`, `IsApproved`, и т. д.

Чтобы отобразить сведения об учетной записи необходимые сведения о пользователе в GridView, установим GridView `AutoGenerateColumns` значение False и добавьте поля BoundField, кроме для `UserName`, `Email`, и `Comment` свойства и CheckBoxFields для `IsApproved`, `IsLockedOut`, и `IsOnline` свойства. Эта конфигурация может применяться посредством декларативная разметка элемента управления или с помощью поля-диалоговое окно. Рис. 3 показан снимок экрана полей диалоговое окно после снят флажок автоматического создания полей и полей BoundField и CheckBoxFields добавлен и настроен.


[![Добавьте три поля BoundFields и три CheckBoxFields к GridView](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**Рис. 3**: Добавьте три поля BoundFields и три CheckBoxFields к GridView ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png))


После настройки к GridView, убедитесь, что его декларативная разметка будет выглядеть примерно:

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

Далее нам нужно написать код, который связывает учетные записи пользователей к GridView. Создайте метод с именем `BindUserAccounts` для выполнения этой задачи, а затем вызвать его из `Page_Load` обработчик событий при первом посещении страницы.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

Отвлекитесь и проверьте страницу в обозревателе. Как показано на рис. 4, `UserAccounts` GridView перечисляет имя пользователя, адрес электронной почты и других соответствующих учетных записей для всех пользователей в системе.


[![Учетные записи пользователей указаны в GridView](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**Рис. 4**: Учетные записи пользователей указаны в GridView ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png))


## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>Шаг 3. Фильтрация результатов по первой букве имени пользователя

В настоящее время `UserAccounts` показывает GridView *все* учетных записей пользователей. Для веб-сайтов с сотнями или тысячами учетных записей пользователей крайне важно, этот пользователь сможет быстро сократить отображаемых учетных записей. Это можно сделать, добавив фильтрации элементов управления LinkButton на страницу. Давайте добавим 27 элементов управления LinkButton на страницу: один под названием все вместе с одной LinkButton для каждой буквы алфавита. При выборе всех LinkButton, GridView Показать всех пользователей. При нажатии кнопки определенной буквы, будет отображаться только тем пользователям, ее имя пользователя начинается с выбранной буквы.

Наша первая задача является добавление 27 элементы управления LinkButton. Один из вариантов является создание элементов управления LinkButton 27 декларативно, по одному. Более гибкий подход является использование элемента управления Repeater с `ItemTemplate` , отображает LinkButton, а затем привязывает параметры фильтрации к элементу управления Repeater, как `String` массива.

Начните с добавления элемента управления Repeater к странице выше `UserAccounts` GridView. Задать элементу управления Repeater `ID` свойства `FilteringUI` Настройка шаблонов элементу управления Repeater, чтобы его `ItemTemplate` отображает LinkButton которого `Text` и `CommandName` свойства привязаны к текущему элементу массива. Как мы видели в <a id="_msoanchor_3"> </a> [ *назначение ролей пользователям* ](../roles/assigning-roles-to-users-vb.md) учебника, это можно сделать с помощью `Container.DataItem` синтаксис привязки данных. Использование элемента Repeater `SeparatorTemplate` для отображения вертикальную линию между каждой ссылки.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

Для заполнения этого элемента управления Repeater с требуемыми параметрами фильтрации, создайте метод с именем `BindFilteringUI`. Вызовите этот метод из `Page_Load` обработчик событий при первой загрузке страницы.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

Этот метод задает параметры фильтрации, как элементы в `String` массива `filterOptions` для каждого элемента в массиве, элементу управления Repeater будет отображаться LinkButton с его `Text` и `CommandName` свойствами, назначенными значение массива элемент.

Рис. 5 показан `ManageUsers.aspx` страницы при просмотре в обозревателе.


[![Элемент управления Repeater перечисляет 27 фильтрации элементов управления LinkButton](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**Рис. 5**: Элемент управления Repeater перечисляет 27 фильтрации элементов управления LinkButton ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png))


> [!NOTE]
> Имена пользователей может начинаться с любого символа, включая цифр и знаков препинания. Чтобы просмотреть эти учетные записи, администратор будет использовать параметр всех LinkButton. Кроме того можно добавить LinkButton, чтобы вернуть все учетные записи пользователей, которые начинаются с цифры. Оставить этот в качестве упражнения для чтения.


Щелкнув любой фильтрации элементов управления LinkButton, вызывает обратную передачу и вызывает элементу управления Repeater `ItemCommand` событий, но никак не изменяется в сетке, так как еще не писать код для фильтрации результатов. `Membership` Класс включает [ `FindUsersByName` метод](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) , возвращает эти учетные записи пользователей, имена которых соответствует указанному шаблону поиска. Этот метод можно использовать для получения только те учетные записи пользователей, которых имена пользователей начинаются с буквы, определяемое `CommandName` из отфильтрованных LinkButton, которая была нажата.

Начните с обновления `ManageUser.aspx` класса кода программной части страницы, теперь она содержит свойство с именем `UsernameToMatch` это свойство сохраняет строку фильтра имени пользователя во время обратной передачи:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

`UsernameToMatch` Свойство сохраняет его значение, оно назначается в `ViewState` коллекции с помощью ключа UsernameToMatch. При чтении значение этого свойства, он проверяет, существует ли значение в `ViewState` коллекции; в противном случае он возвращает значение по умолчанию — пустая строка. `UsernameToMatch` Свойство будет проявлять общий шаблон, а именно сохранение значения состояния представления, чтобы любые изменения свойства сохраняются во время обратной передачи. Дополнительные сведения об этом шаблоне [Общие сведения о состоянии представления ASP.NET](https://msdn.microsoftn-us/library/ms972976.aspx).

Затем обновите `BindUserAccounts` метод так, чтобы вместо вызова метода `Membership.GetAllUsers`, он вызывает `Membership.FindUsersByName`, передавая значение `UsernameToMatch` свойство с символом-шаблоном SQL, %.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

Чтобы отобразить только те пользователи, ее имя пользователя начинается с буквы А, задайте `UsernameToMatch` свойства для типа, а затем вызвать `BindUserAccounts` это может привести к вызову `Membership.FindUsersByName("A%")`, который возвращает всех пользователей, имена которых начинаются с а. аналогичным образом, чтобы вернуть *все* пустую строку, чтобы назначить пользователей, `UsernameToMatch` свойство, чтобы `BindUserAccounts` метод будет вызывать `Membership.FindUsersByName("%")`, тем самым возврат всех учетных записей пользователей.

Создайте обработчик событий для элемента управления Repeater `ItemCommand` событий. Это событие возникает при каждом нажатии одной из фильтра элементов управления LinkButton; он передается щелкнули LinkButton `CommandName` значение через `RepeaterCommandEventArgs` объекта. Нам нужно назначить соответствующее значение для `UsernameToMatch` свойства, а затем вызовите метод `BindUserAccounts` метод. Если `CommandName` — это все, пустую строку, чтобы назначить `UsernameToMatch` , отображаются все учетные записи пользователей. В противном случае — назначить `CommandName` значение `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

Этот код в месте тестирование функций фильтрации. При первом посещении страницы, отображаются все учетные записи пользователей (см. рис. 5). Щелчок LinkButton вызывает обратную передачу и фильтрует результаты, отображение только учетные записи пользователей, которые начинаются с A.


[![Используется для отображения этих пользователей, имена которых начинаются с определенной буквы фильтрации элементов управления LinkButton](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**Рис. 6**: Использование элементов управления LinkButton фильтрации для отображения этих пользователей которых имя пользователя начинается с некоторые буквы ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png))


## <a name="step-4-updating-the-gridview-to-use-paging"></a>Шаг 4. Обновляется GridView использовать разбиение на страницы

GridView, показанный на рис. 5 и 6 перечисляет все записи, возвращенные из `FindUsersByName` метод. Если существуют сотни или тысячи учетных записей пользователей это может привести к информационной перегрузке при просмотре всех учетных записей (как в случае при нажатии кнопки LinkButton все или при первоначальном просмотре странице). Чтобы представить учетные записи пользователей в виде более управляемых блоков, давайте настроим GridView для отображения 10 учетных записей пользователей одновременно.

Элемент управления GridView обеспечивает два вида разбиения на страницы:

- **Разбиение по страницам по умолчанию** — легко реализовать, но неэффективно. По сути, разбиение по страницам GridView имеет значения по умолчанию ожидает *все* записи из источника данных. Оно только отображает соответствующую страницу записей.
- **Пользовательское разбиение по страницам** -требует больше усилий для реализации, но более эффективным, чем разбиение по страницам по умолчанию, так как с помощью пользовательского разбиения по страницам данных источник возвращает только точного набора записей для отображения.

Разница в производительности по умолчанию и пользовательское разбиение по страницам могут быть довольно значительными, если разбиение по страницам тысячи записей. Поскольку мы создаем этот интерфейс, при условии, что существует могут быть сотни или тысячи учетных записей пользователей, мы используем пользовательское разбиение по страницам.

> [!NOTE]
> Более подробные сведения о различиях между по умолчанию и пользовательское разбиение по страницам, а также о проблемах, связанных с реализации пользовательского разбиения по страницам, см. в разделе [эффективного разбиения на страницы через больших объемов данных](https://asp.net/learn/data-access/tutorial-25-vb.aspx). Анализ производительности разницу по умолчанию и пользовательское разбиение по страницам, см. в разделе [пользовательское разбиение по страницам в ASP.NET с помощью SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx).


Чтобы реализовать пользовательское разбиение по страницам, необходимо сначала какого-либо механизма, используемого для получения нужного подмножества записей, отображаемых GridView. Хорошая новость в том, что `Membership` класса `FindUsersByName` метод имеет перегрузку, можно указать индекс страницы и размера страницы и возвращает только учетные записи пользователей, которые попадают в этот диапазон записей.

В частности, эта перегрузка имеет следующую сигнатуру: [ `FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)` ](https://msdn.microsoft.com/library/fa5st8b2.aspx).

*PageIndex* параметр указывает на страницу учетных записей пользователей для возвращения; *pageSize* указывает число записей, отображаемых на одной странице. *TotalRecords* параметр `ByRef` параметром, возвращающим число учетных записей пользователей в хранилище пользователя.

> [!NOTE]
> Данные, возвращаемые `FindUsersByName` сортируется по имени пользователя; невозможно настроить критерии сортировки.


Чтобы использовать пользовательское разбиение по страницам, но только при привязке к элементу управления ObjectDataSource можно настроить GridView. Для элемента управления ObjectDataSource для реализации пользовательского разбиения по страницам, требуется два метода: один, передаваемый индекс начальной строки и максимальное число записей для отображения, и возвращает точные подмножества записей, которые попадают в этой области. и метод, который возвращает общее число записей, разбиваемых по страницам. `FindUsersByName` Перегрузка принимает индекс страницы и размера страницы и возвращает общее число записей с помощью `ByRef` параметра. Поэтому имеется несовпадение интерфейс здесь.

Один из вариантов является создание класса прокси-сервера, предоставляющей интерфейс ObjectDataSource ожидает, что и процедура автоматически вызывает `FindUsersByName` метод. Другой вариант — и мы будем использовать для этой статьи один — является создание нашего собственного интерфейса разбиения по страницам и используют его вместо элемента GridView встроенный интерфейс разбиения по страницам.

### <a name="creating-a-first-previous-next-last-paging-interface"></a>Во-первых, создание предыдущая, затем последнего интерфейса разбиения по страницам

Давайте создадим интерфейс разбиения по страницам с первой, назад, Далее и последнего элементов управления LinkButton. Первого элемента управления LinkButton, при нажатии будет переводить пользователя на первую страницу данных, тогда как предыдущие вернет ему на предыдущую страницу. Аналогичным образом Далее» и «Дата последнего будет перевести пользователя на страницу следующим и последним соответственно. Добавьте четыре элемента управления LinkButton, под `UserAccounts` GridView.

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

Создайте обработчик событий для каждого из LinkButton `Click` события.

Рис. 7 показаны четыре элементов управления LinkButton при просмотре через представление Visual Web Developer Design.


[![Затем добавьте во-первых, предыдущего, и последнего элементов управления LinkButton под GridView](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**Рис. 7**: Во-первых, добавьте назад, Next и последнего элементов управления LinkButton под GridView ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png))


### <a name="keeping-track-of-the-current-page-index"></a>Слежении за индекс текущей страницы

При первом посещении `ManageUsers.aspx` страницы или щелчков мыши один из фильтрация кнопок, мы должны отображаться на первой странице данных в GridView. Когда пользователь нажимает одну из навигации элементов управления LinkButton, тем не менее, необходимо обновить индекс страницы. Чтобы сохранить индекс страницы и количество записей, отображаемых на каждой странице, добавьте следующие два свойства класса фонового кода страницы:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

Как и `UsernameToMatch` свойства `PageIndex` свойство сохраняется его значение состояния представления. Только для чтения `PageSize` свойство возвращает жестко запрограммированных значений, 10. Я приглашаю интересующихся обновить это свойство для использования той же схеме, что `PageIndex`, а затем дополнить `ManageUsers.aspx` странице таким образом, что лица, посетив страницу можно указать, сколько учетных записей пользователей, отображаемых на одной странице.

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>Извлечение только записи текущей страницы, обновления индекса страницы и включение и отключение элементов управления LinkButton интерфейс разбиения по страницам

С помощью интерфейса разбиения по страницам на месте и `PageIndex` и `PageSize` добавлены свойства, мы готовы обновить `BindUserAccounts` метод использования соответствующего `FindUsersByName` перегрузки. Кроме того необходимо иметь этот метод включает или отключает интерфейс разбиения по страницам в зависимости от того, какой экран. При просмотре первой страницы данных, следует отключить ссылки первый» и «назад; Далее и последнего должен быть отключен, при просмотре на последней странице.

Обновите метод `BindUserAccounts`, используя следующий код:

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

Обратите внимание, что общее число записей, разбиваемых по страницам определяется в последнем параметре `FindUsersByName` метод. После возвращения указанную страницу учетных записей пользователей, четырех элементов управления LinkButton включены или отключены, в зависимости от того, просматривается ли к первой или последней странице данных.

Последним шагом является написание кода для четырех элементов управления LinkButton `Click` обработчики событий. Эти обработчики событий необходимо обновить `PageIndex` свойство и затем привяжите данные к элементу GridView через вызов `BindUserAccounts` первой, предыдущую и следующую обработчики событий — это очень простой. `Click` Обработчик событий для последнего элемента управления LinkButton, тем не менее, немного сложнее, так как нам нужно определить, сколько записей отображаются для определения последнего индекса страницы.

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

Цифры 8 и 9 Показать пользовательский интерфейс разбиения на страницы в действии. На рисунке 8 показана `ManageUsers.aspx` страницы при просмотре первой страницы данных для всех учетных записей пользователей. Обратите внимание на то, что отображаются только 10 из 13 учетных записей. Щелкнув ссылку Далее или последнего вызывает обратную передачу, обновления `PageIndex` 1, и второй странице пользователя, учетные записи в сетку привязки (см. рис. 9).


[![Отображаются первая учетные записи пользователей 10](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**Рис. 8**: Первый учетные записи пользователей 10 отображаются ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png))


[![Щелчок следующей ссылки отображаются на второй странице учетных записей пользователей](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**Рис. 9**: Щелчок следующей ссылки отображаются на второй странице из учетных записей пользователей ([Просмотр полноразмерного изображения](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png))


## <a name="summary"></a>Сводка

Администраторам часто нужно выбрать из списка учетных записей пользователя. В предыдущих учебных курсах рассматривалось использование раскрывающегося списка, заполняется с пользователями, но этот подход не может хорошо масштабироваться. В этом руководстве мы изучили лучшая альтернатива: фильтруемых интерфейс, результаты которого отображаются в разбитых на страницы элемента управления GridView. С этим интерфейсом пользователя администраторы могут быстро и эффективно найдите и выберите одну учетную запись пользователя среди тысяч.

Счастливого вам программирования!

### <a name="further-reading"></a>Дополнительные сведения

Дополнительные сведения по темам, обсуждавшимся в этом руководстве см. в следующих ресурсах:

- [Пользовательское разбиение по страницам в ASP.NET с помощью SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [Эффективное разбиение больших объемов данных](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [Развертывание собственного средства администрирования веб-сайта](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>Об авторе

Скотт Митчелл, автор нескольких книг по ASP/ASP.NET и основатель веб-узла 4GuysFromRolla.com, работает с веб-технологиями Microsoft с 1998 года. Скотт — независимый консультант, преподаватель и автор. Его последняя книга —  *[Sams Teach ASP.NET 2.0 in 24 часа](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*. Скоттом можно связаться по адресу [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) или через его блог по адресу [ http://ScottOnWriting.NET ](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Особая благодарность

В этой серии руководств пособий рецензировалась многими компетентными редакторами. Основной рецензент этого учебного был Alicja Maziarz. Хотите поработать с моих последующих статей для MSDN? Если Да, напишите мне

> [!div class="step-by-step"]
> [Назад](unlocking-and-approving-user-accounts-cs.md)
> [Вперед](recovering-and-changing-passwords-vb.md)