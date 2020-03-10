---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC (часть 2) | Документация Майкрософт
author: Rick-Anderson
description: В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в ASP.NET МВ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498420"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>Использование HTML5 и всплывающего календаря DatePicker в элементе пользовательского интерфейса jQuery с ASP.NET MVC. часть 2

по [Рик Андерсон (](https://twitter.com/RickAndMSFT)

> В этом учебнике вы узнаете, как работать с шаблонами редактора, шаблонами отображения и всплывающим календарем Datepicker пользовательского интерфейса jQuery в веб-приложении ASP.NET MVC.

## <a name="adding-an-automatic-datetime-template"></a>Добавление автоматического шаблона даты и времени

В первой части этого руководства вы узнали, как добавить атрибуты в модель, чтобы явно указать форматирование, и как можно явно указать шаблон, используемый для отрисовки модели. Например, атрибут [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) в следующем коде явно определяет форматирование для свойства `ReleaseDate`.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

В следующем примере атрибут [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , использующий перечисление `Date`, указывает, что шаблон даты должен использоваться для отрисовки модели. Если в проекте нет шаблона даты, используется встроенный шаблон даты.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

Однако ASP. MVC может выполнять сопоставление типов, используя соглашение-over-Configuration, путем поиска шаблона, соответствующего имени типа. Это позволяет создать шаблон, который автоматически форматирует данные без использования каких-либо атрибутов или кода. В этой части руководства вы создадите шаблон, который автоматически применяется к свойствам модели типа [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx). Не нужно использовать атрибут или другую конфигурацию, чтобы указать, что шаблон должен использоваться для отрисовки всех свойств модели типа [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx).

Кроме того, вы узнаете, как настроить отображение отдельных свойств или даже отдельных полей.

Для начала удалим существующие сведения о форматировании и отобразите полные даты в приложении.

Откройте файл *Movie.CS* и закомментируйте атрибут `DataType` в свойстве `ReleaseDate`:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

Для запуска приложения нажмите сочетание клавиш CTRL+F5.

Обратите внимание, что свойство `ReleaseDate` теперь отображает дату и время, так как это значение по умолчанию, если сведения о форматировании не предоставлены.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>Добавление стилей CSS для тестирования новых шаблонов

Перед созданием шаблона для форматирования дат необходимо добавить несколько правил стиля CSS, которые можно применить к новым шаблонам. Они помогут проверить, использует ли подготовленная страница новый шаблон.

Откройте файл *контент\сите.КС*s и добавьте следующие правила CSS в нижнюю часть файла:

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>Добавление шаблонов для вывода даты и времени

Теперь можно создать новый шаблон. В папке *виевс\мовиес* создайте папку *DisplayTemplates* .

В папке *Views\Shared* создайте папку *DisplayTemplates* и папку *EditorTemplates* .

Шаблоны вывода в папке *views\shared\displaytemplates.* будут использоваться всеми контроллерами. Шаблоны вывода в папке *виевс\мовие\дисплайтемплатес* будут использоваться только контроллером `Movie`. (Если шаблон с таким же именем отображается в обеих папках, шаблон в папке *виевс\мовие\дисплайтемплатес* , то есть более конкретный шаблон, имеет приоритет для представлений, возвращаемых контроллером `Movie`.)

В **Обозреватель решений**разверните папку *представления* , разверните *общую* папку, а затем щелкните правой кнопкой мыши папку *views\shared\displaytemplates.* .

Нажмите кнопку **Добавить** , а затем — **вид**. Откроется диалоговое окно **Добавление представления** .

В поле **имя представления** введите `DateTime`. (Для сопоставления имени типа необходимо использовать это имя.)

Установите флажок **создать как частичное представление** . Убедитесь, что не установлены флажки **использовать макет или эталонную страницу** и **создать строго типизированное представление** .

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

Нажмите кнопку **Добавить**. Шаблон *DateTime. cshtml* создается в *views\shared\displaytemplates.* .

На следующем рисунке показана папка *views* в **обозреватель решений** после создания `DateTime` шаблонов отображения и редактора.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

Откройте файл *виевс\шаред\дисплайтемплатес\датетиме.кштмл* и добавьте следующую разметку, которая использует метод [String. Format](https://msdn.microsoft.com/library/system.string.format.aspx) для форматирования свойства как даты без времени. (Формат `{0:d}` задает короткий формат даты.)

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

Повторите этот шаг, чтобы создать шаблон `DateTime` в папке *виевс\мовие\дисплайтемплатес* Используйте следующий код в файле *виевс\мовие\дисплайтемплатес\датетиме.кштмл* .

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

Класс `loud-1` CSS приводит к отображению даты полужирным шрифтом в красном тексте. `loud-1` класс CSS был добавлен как временная мера, чтобы можно было легко увидеть, когда используется этот шаблон.

Вы создали и настроили шаблоны, которые ASP.NET будут использовать для вывода дат. В более общем шаблоне (в папке *views\shared\displaytemplates.* ) отображается простая короткая дата. В шаблоне, специально предназначенном для контроллера `Movie` (в папке *виевс\мовиес\дисплайтемплатес* ), отображается краткая Дата, которая также форматируется полужирным красным текстом.

Для запуска приложения нажмите сочетание клавиш CTRL+F5. Браузер подготавливает представление индекса для приложения.

Свойство `ReleaseDate` теперь отображает дату полужирным шрифтом красного цвета без времени. Это позволяет убедиться, что `DateTime` шаблон вспомогательного метода в папке *виевс\мовиес\дисплайтемплатес* установлен на `DateTime` шаблонной вспомогательной функции в общей папке (*views\shared\displaytemplates.* ).

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

Теперь переименуйте файл *виевс\мовиес\дисплайтемплатес\датетиме.кштмл* в *виевс\мовиес\дисплайтемплатес\лауддатетиме.кштмл*.

Для запуска приложения нажмите сочетание клавиш CTRL+F5.

На этот раз свойство `ReleaseDate` отображает дату без времени и без выделенного полужирного шрифта красного цвета. Это показывает, что шаблон с именем типа данных (в данном случае `DateTime`) автоматически используется для вывода всех свойств модели этого типа. После переименования файла *DateTime. cshtml* в *лауддатетиме. cshtml*ASP.NET больше не будет найден шаблон в папке *виевс\мовиес\дисплайтемплатес* , поэтому он использовал шаблон *DateTime. cshtml* из папки * виевс\мовиес\шаред\*.

(В соответствии с шаблоном регистр не учитывается, поэтому можно было бы создать имя файла шаблона с любым регистром. Например, значения *DateTime. cshtml, DateTime. cshtml*и *DateTime. cshtml* будут соответствовать типу `DateTime`.)

Для проверки: на этом этапе поле `ReleaseDate` отображается с помощью шаблона *виевс\мовиес\дисплайтемплатес\датетиме.кштмл* , который отображает данные в кратком формате даты, но в противном случае не добавляет Специальный формат.

### <a name="using-uihint-to-specify-a-display-template"></a>Использование UIHint для указания шаблона интерфейса

Если веб-приложение содержит много полей `DateTime` и по умолчанию требуется отображать все или большинство из них в формате "только дата", шаблон *DateTime. cshtml* является хорошим подходом. Но что делать, если у вас есть несколько дат, где нужно отобразить полную дату и время? Не беспокойтесь. Можно создать дополнительный шаблон и использовать атрибут [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) , чтобы указать форматирование для полной даты и времени. Затем можно выборочно применить этот шаблон. Можно использовать атрибут [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) на уровне модели или можно указать шаблон внутри представления. В этом разделе вы узнаете, как использовать атрибут `UIHint` для выборочного изменения форматирования некоторых экземпляров полей даты и времени.

Откройте файл *виевс\мовиес\дисплайтемплатес\лауддатетиме.кштмл* и замените существующий код следующим:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

Это приводит к отображению полной даты и времени и добавлению класса CSS, который делает текст зеленым и большим.

Откройте файл *Movie.CS* и добавьте атрибут [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) в свойство `ReleaseDate`, как показано в следующем примере:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

Это говорит ASP.NET MVC о том, что при отображении свойства `ReleaseDate` (в частности, а не только для объекта `DateTime`) он должен использовать шаблон *лауддатетиме. cshtml* .

Для запуска приложения нажмите сочетание клавиш CTRL+F5.

Обратите внимание, что свойство `ReleaseDate` теперь отображает дату и время в большом зеленом шрифте.

Вернитесь к атрибуту `UIHint` в файле *Movie.CS* и закомментируйте его, чтобы шаблон *лауддатетиме. cshtml* не использовался. Повторный запуск приложения Дата выпуска не отображается как крупная и зеленая. Это подтверждает, что шаблон *виевс\шаред\дисплайтемплатес\датетиме.кштмл* используется в представлениях индекса и сведений.

Как упоминалось ранее, можно также применить шаблон в представлении, который позволяет применить шаблон к отдельному экземпляру некоторых данных. Откройте представление *виевс\мовиес\детаилс.кштмл* . Добавьте `"LoudDateTime"` в качестве второго параметра вызова [HTML. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) для поля `ReleaseDate`. Завершенный код выглядит следующим образом:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

Это означает, что шаблон `LoudDateTime` должен использоваться для вывода свойства модели независимо от того, какие атрибуты применяются к модели.

Для запуска приложения нажмите сочетание клавиш CTRL+F5.

Убедитесь, что страница индекса фильма использует шаблон *виевс\шаред\дисплайтемплатес\датетиме.кштмл* (выделяется красным шрифтом), а страница *Мовие\детаилс* использует шаблон *виевс\мовиес\дисплайтемплатес\лауддатетиме.кштмл* (крупный и зеленый).

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

В следующем разделе вы создадите шаблон для сложного типа.

> [!div class="step-by-step"]
> [Назад](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [Вперед](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
