---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Создание приложения MVC 3 с помощью Razor и ненавязчивого JavaScript | Документация Майкрософт
author: microsoft
description: Пример веб-приложения "список пользователей" демонстрирует, как просто создавать приложения ASP.NET MVC 3 с помощью подсистемы представлений Razor. Пример приложения s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435000"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Создание приложения на MVC 3 с помощью Razor и ненавязчивого JavaScript

по [Майкрософт](https://github.com/microsoft)

> Пример веб-приложения "список пользователей" демонстрирует, как просто создавать приложения ASP.NET MVC 3 с помощью подсистемы представлений Razor. В примере приложения показано, как использовать новый модуль представлений Razor с ASP.NET MVC версии 3 и Visual Studio 2010 для создания вымышленного веб-сайта списка пользователей, который включает такие функции, как создание, отображение, изменение и удаление пользователей.
> 
> В этом учебнике описываются шаги, которые были выполнены для создания примера приложения ASP.NET MVC 3 в списке пользователей. Проект Visual Studio с C# исходным кодом VB можно найти в этой статье: [download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114). Если у вас возникли вопросы по этому учебнику, опубликуйте их на [форуме MVC](https://forums.asp.net/1146.aspx).

## <a name="overview"></a>Обзор

Создаваемое приложение — это простой веб-сайт списка пользователей. Пользователи могут вводить, просматривать и обновлять сведения о пользователях.

![Образец сайта](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

Вы можете скачать VB и C# готовый проект [здесь](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).

## <a name="creating-the-web-application"></a>Создание веб-приложения

Чтобы начать работу с руководством, откройте Visual Studio 2010 и создайте новый проект с помощью шаблона *веб-приложения ASP.NET MVC 3* . Присвойте приложению имя &quot;Mvc3Razor&quot;.

[![новый проект MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

В диалоговом окне **Новый проект ASP.NET MVC 3** выберите **Интернет приложение**, выберите подсистему представлений Razor и нажмите кнопку **ОК**.

![Диалоговое окно создания проекта ASP.NET MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

В этом учебнике вы не будете использовать поставщик членства ASP.NET, поэтому вы можете удалить все файлы, связанные с входом и членством. В **Обозреватель решений**удалите следующие файлы и каталоги:

- *контроллерс\аккаунтконтроллер*
- *моделс\аккаунтмоделс*
- *Views\Shared\\_LogOnPartial*
- *Виевс\аккаунт* (и все файлы в этом каталоге)

![Солн exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

Измените файл <em>\_Layout. cshtml</em> и замените разметку внутри элемента `<div>` с именем `logindisplay` на сообщение <em>&quot;</em>login Disabled&quot;. В следующем примере показана новая разметка:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>Добавление модели

В **Обозреватель решений**щелкните правой кнопкой мыши папку *модели* , выберите **добавить**, а затем выберите **класс**.

![Новый класс пользовательского MDL](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

Назовите класс `UserModel`. Замените содержимое файла *усермодел* следующим кодом:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

Класс `UserModel` представляет пользователей. Каждый член класса снабжается атрибутом [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) из пространства имен [Annotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) . Атрибуты в пространстве имен [Annotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) обеспечивают автоматическую проверку на стороне клиента и сервера для веб-приложений.

Откройте класс `HomeController` и добавьте директиву `using`, чтобы получить доступ к классам `UserModel` и `Users`:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

Сразу после объявления `HomeController` добавьте следующий комментарий и ссылку на `Users` класс:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

Класс `Users` — это упрощенное хранилище данных в памяти, которое будет использоваться в этом руководстве. В реальных приложениях для хранения сведений о пользователях используется база данных. Первые несколько строк файла `HomeController` показаны в следующем примере:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

Создайте приложение, чтобы модель пользователя была доступна в мастере формирования шаблонов на следующем шаге.

## <a name="creating-the-default-view"></a>Создание представления по умолчанию

Следующим шагом является Добавление метода действия и представления для отображения пользователей.

Удалите существующий файл *виевс\хоме\индекс* . Вы создадите новый файл *индекса* для просмотра пользователей.

В классе `HomeController` замените содержимое метода `Index` следующим кодом:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

Щелкните правой кнопкой мыши внутри метода `Index` и выберите **Добавить представление**.

![Добавить представление](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

Выберите параметр **создать строго типизированное представление** . В качестве **класса данных представления**выберите **Mvc3Razor. Models. усермодел**. (Если в поле **класс представления** не отображается **Mvc3Razor. Models. усермодел** , необходимо выполнить сборку проекта.) Убедитесь, что для обработчика представлений задано значение **Razor**. Задайте для параметра **Просмотреть содержимое** значение **список** и нажмите кнопку **добавить**.

![Добавить представление индекса](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

Новое представление автоматически формирует формирование шаблонов пользовательских данных, которые передаются в представление `Index`. Изучите только что созданный файл *виевс\хоме\индекс* . Ссылки **создать**, **изменить**, **Подробности**и **Удалить** не работают, но остальная часть страницы функционирует. Запустите страницу. Отобразится список пользователей.

![Страница индекса](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

Откройте файл *index. cshtml* и замените разметку `ActionLink` для **Edit**, **Details**и **Delete** следующим кодом:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

Имя пользователя используется в качестве идентификатора для поиска выбранной записи в ссылках **Edit**, **Details**и **Delete** .

## <a name="creating-the-details-view"></a>Создание представления сведений

Следующим шагом является Добавление метода действия `Details` и представления для отображения сведений о пользователе.

![Сведения](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

Добавьте следующий метод `Details` к контроллеру Home:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

Щелкните правой кнопкой мыши внутри метода `Details` и выберите <strong>Добавить представление</strong>. Убедитесь, что поле <strong>класс данных представления</strong> содержит <strong>Mvc3Razor. Models. усермодел</strong><em>.</em> Задайте <strong>сведения о</strong> <strong>содержимом представления</strong> и нажмите кнопку <strong>добавить</strong>.

![Добавить представление сведений](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

Запустите приложение и выберите ссылку сведения. При автоматическом формировании шаблонов отображается каждое свойство модели.

![Сведения](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>Создание представления редактирования

Добавьте следующий метод `Edit` в контроллер Home.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

Добавьте представление, как в предыдущих шагах, но задайте для параметра **Просмотр содержимого** значение **изменить**.

![Добавить представление редактирования](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

Запустите приложение и измените имя и фамилию одного из пользователей. При нарушении ограничений `DataAnnotation`, примененных к классу `UserModel`, при отправке формы будут отображаться ошибки проверки, вызванные кодом сервера. Например, если изменить имя &quot;Анна&quot; на &quot;&quot;, то при отправке формы в форме отобразится следующая ошибка:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

В этом руководстве вы имя пользователя в качестве первичного ключа. Поэтому свойство имени пользователя не может быть изменено. В файле *Edit. cshtml* сразу после инструкции `Html.BeginForm` задайте имя пользователя как скрытое поле. Это приводит к передаче свойства в модель. В следующем фрагменте кода показано размещение оператора `Hidden`:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

Замените `TextBoxFor` и `ValidationMessageFor` разметку имени пользователя на вызов `DisplayFor`. Метод `DisplayFor` отображает свойство как элемент только для чтения. В следующем примере приведена полная разметка. Первоначальные вызовы `TextBoxFor` и `ValidationMessageFor` заносятся в комментарий с помощью символов начала и конца комментария Razor (`@* *@`)

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>Включение проверки на стороне клиента

Чтобы включить проверку на стороне клиента в ASP.NET MVC 3, необходимо установить два флага и включить три файла JavaScript.

Откройте файл *Web. config* приложения. Убедитесь, что в параметрах приложения `that ClientValidationEnabled` и `UnobtrusiveJavaScriptEnabled` установлены в значение true. В следующем фрагменте из корневого файла *Web. config* отображаются правильные параметры:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

Установка значения "true" `UnobtrusiveJavaScriptEnabled` "включает ненавязчивую проверку AJAX и незаметное клиентская проверка. При использовании ненавязчивой проверки правила проверки преобразуются в атрибуты HTML5. Имена атрибутов HTML5 могут состоять только из строчных букв, цифр и дефисов.

Установка значения true для `ClientValidationEnabled` включает проверку на стороне клиента. Настроив эти ключи в файле *Web. config* приложения, вы включите проверку клиента и ненавязчивый JavaScript для всего приложения. Можно также включить или отключить эти параметры в отдельных представлениях или в методах контроллера, используя следующий код:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

Кроме того, в представление, подготовленное для просмотра, необходимо включить несколько файлов JavaScript. Простой способ включить JavaScript во все представления — добавить их в файл *Views\Shared\\_layout. cshtml* . Замените\_элемент `<head>` файла *Layout. cshtml* следующим кодом:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

Первые два сценария jQuery размещаются в сети доставки содержимого (CDN) Microsoft AJAX. Используя преимущества сети доставки содержимого Microsoft AJAX, вы можете значительно повысить производительность ваших приложений при первом нажатии.

Запустите приложение и щелкните ссылку Edit (изменить). Просмотрите исходный код страницы в браузере. В источнике обозревателя показано множество атрибутов формы `data-val` (для проверки данных). Если проверка клиента и ненавязчивый JavaScript включены, поля ввода с правилом проверки клиента содержат атрибут `data-val="true"`, чтобы активировать ненавязчивую проверку клиента. Например, поле `City` в модели было дополнено [требуемым](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) атрибутом, результатом которого является код HTML, показанный в следующем примере:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

Для каждого правила проверки клиента добавляется атрибут, имеющий форму `data-val-rulename="message"`. Используя приведенный ранее пример поля `City`, необходимое правило проверки клиента создает атрибут `data-val-required` и сообщение, &quot;поле City обязательно&quot;. Запустите приложение, измените одного из пользователей и очистите поле `City`. При выходе из поля вы увидите сообщение об ошибке проверки на стороне клиента.

![Требуется город](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

Аналогичным образом для каждого параметра в правиле проверки клиента добавляется атрибут, имеющий форму `data-val-rulename-paramname=paramvalue`. Например, свойство `FirstName` записывается атрибутом [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) и задает минимальную длину, равную 3, и максимальную длину 8. Правило проверки данных с именем `length` имеет имя параметра `max` и значение параметра 8. Ниже показан код HTML, созданный для поля `FirstName` при изменении одного из пользователей.

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

Дополнительные сведения о ненавязчивой проверке клиента см. в блоге Михаил Уилсон (, посвященном записи [ненавязчивой проверки клиента в ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) .

> [!NOTE]
> В бета-версии ASP.NET MVC 3 иногда необходимо отправить форму, чтобы начать проверку на стороне клиента. Это может быть изменено для окончательного выпуска.

## <a name="creating-the-create-view"></a>Создание представления создания

Следующим шагом является Добавление метода действия `Create` и представления, чтобы позволить пользователю создать нового пользователя. Добавьте следующий метод `Create` к контроллеру Home:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

Добавьте представление, как в предыдущих шагах, но задайте для параметра **представление содержимое** значение **создать**.

![Создание представления](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

Запустите приложение, выберите ссылку **создать** и добавьте нового пользователя. Метод `Create` автоматически использует преимущества проверки на стороне клиента и на стороне сервера. Попробуйте ввести имя пользователя, содержащее пробелы, например &quot;Бен X&quot;. При выходе из поля "имя пользователя" отображается ошибка проверки на стороне клиента (`White space is not allowed`).

## <a name="add-the-delete-method"></a>Добавление метода Delete

Чтобы завершить работу с этим руководством, добавьте следующий метод `Delete` к контроллеру Home:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

Добавьте `Delete` представление, как в предыдущих шагах, указав **содержимое представления** для **удаления**.

![Удалить представление](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

Теперь у вас есть простое, но полностью функциональное приложение ASP.NET MVC 3 с проверкой.
