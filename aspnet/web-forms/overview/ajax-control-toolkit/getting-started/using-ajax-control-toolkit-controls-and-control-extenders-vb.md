---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: Использование элементов управления AJAX Control Toolkit и расширителей элементов управления (VB) | Документация Майкрософт
author: microsoft
description: Узнайте, как добавить элементы управления AJAX Control Toolkit и средства расширения на страницы ASP.NET.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 90a6003ff50ba6e85196c25cf175e057810f0f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497052"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>Использование элементов управления из набора элементов AJAX и управляющих элементов-расширителей (VB)

по [Майкрософт](https://github.com/microsoft)

> Узнайте, как добавить элементы управления AJAX Control Toolkit и средства расширения на страницы ASP.NET.

AJAX Control Toolkit содержит набор элементов управления и расширителей элементов управления. В этом кратком руководстве вы узнаете, как добавлять элементы управления и расширители элементов управления на страницу ASP.NET.

> [!NOTE] 
> 
> Инструкции по установке AJAX Control Toolkit и добавлению набора средств AJAX Control Toolkit в область элементов Visual Studio/Visual Web Developer см. в руководстве [Приступая к работе с набором средств AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb.md).

## <a name="using-ajax-control-toolkit-controls"></a>Использование элементов управления AJAX Control Toolkit

Элемент управления AJAX Control Toolkit работает так же, как и стандартный элемент управления ASP.NET. Элемент управления можно перетащить с панели элементов на страницу ASP.NET. Элемент управления можно добавить на страницу либо в представление конструирования, либо в представлении исходного кода.

При использовании элементов управления из набора AJAX Control Toolkit существует одно специальное требование. Страница должна содержать элемент управления ScriptManager. Элемент управления ScriptManager отвечает за включение всех необходимых сценариев JavaScript для элементов управления AJAX Control Toolkit.

Например, вкладка AJAX Control Toolkit содержит элемент управления, именуемый элементом управления редактора. Этот элемент управления отображает форматированный HTML-редактор. Чтобы добавить элемент управления редактора на страницу, выполните следующие действия.

1. Создание новой страницы ASP.NET с именем Шоведитор. aspx
2. Выберите элемент управления ScriptManager из вкладки расширения AJAX на панели элементов и перетащите элемент управления на страницу.
3. Выберите элемент управления редактора, расположенный под вкладкой AJAX Control Toolkit на панели элементов, и перетащите элемент управления на страницу (см. рис. 1). Конструктор должен выглядеть, как показано на рис. 2.
4. Запустите веб-сайт, выбрав пункт меню **Отладка, начать отладку** или нажав клавишу F5.
5. Страница показана на рис. 3.

[![выбора элемента управления редактора HTML](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**Рис. 01**. Выбор элемента управления редактора HTML ([щелкните, чтобы просмотреть изображение с полным размером](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))

[![конструктора Visual Studio с помощью элементов управления ScriptManager и Edit](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**Рис. 02**. конструктор Visual Studio с ScriptManager и Edit Control ([щелкните, чтобы просмотреть изображение с полным размером](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))

[![страницы Дисплайедитор. aspx](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**Рис. 03**. страница дисплайедитор. aspx ([щелкните, чтобы просмотреть изображение с полным размером](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>Использование расширителей элемента управления AJAX Control Toolkit

Набор элементов управления AJAX также содержит расширители элементов управления. Как видно из названия, расширитель элемента управления расширяет функциональные возможности существующего элемента управления. Например, расширитель элемента управления ConfirmButton расширяет стандартный элемент управления "кнопка ASP.NET". Расширитель изменяет поведение элемента управления "Кнопка", чтобы при нажатии кнопки отображалось диалоговое окно подтверждения.

Для расширения элемента управления, как и элемента управления AJAX Control Toolkit, требуется элемент управления ScriptManager. Перед началом использования расширителей элементов управления на странице необходимо добавить элемент управления ScriptManager на страницу.

Выполните следующие действия, чтобы использовать расширитель элемента управления ConfirmButton:

1. Создание новой страницы ASP.NET с именем Шовконфирмбуттон. aspx
2. Добавьте элемент управления ScriptManager на страницу, перетащив элемент управления на страницу с вкладки расширения AJAX.
3. Добавьте на страницу стандартный элемент управления "Кнопка", перетащив кнопку со страницы "стандартные" в области элементов на поверхность конструктора.
4. Щелкните параметр **Добавить задачу расширения** (см. рис. 4).
5. В диалоговом окне Выбор расширителя выберите Конфирмбуттонекстендер (см. рис. 5) и нажмите кнопку ОК.
6. Выберите элемент управления "Кнопка" в конструкторе и разверните узел расширители, Button1\_Конфирмбуттонекстендер в окно свойств (см. рис. 6). Присвоить значение *действительно?* свойству конфирмтекст.
7. Запустите страницу, выбрав пункт меню **Отладка, начать отладку** или нажать клавишу F5.

[![параметра задачи «Добавление расширителя»](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**Рис. 04**. параметр задачи «Добавление расширения» ([щелкните, чтобы просмотреть изображение с полным размером](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))

[![выбора расширителя элемента управления ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**Рис. 05**. Выбор расширителя элемента управления ConfirmButton ([щелкните, чтобы просмотреть изображение с полным размером](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))

[![установки свойства ConfirmButton](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**Рис. 06**. Задание свойства ConfirmButton ([щелкните, чтобы просмотреть изображение с полным размером](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))

При открытии страницы появится кнопка. При нажатии кнопки появляется диалоговое окно подтверждения на рис. 7.

[![отображения диалогового окна подтверждения](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**Рис. 07**. Отображение диалогового окна подтверждения ([щелкните, чтобы просмотреть изображение с полным размером](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))

Обратите внимание, что обычно не выполняется перетаскивание расширителя элемента управления на страницу. Вместо этого используйте параметр Добавить задачу- **расширитель** , чтобы добавить расширитель к элементу управления, который уже добавлен на страницу. Кроме того, обратите внимание, что вы настроили свойства расширителя элементов управления, открыв вкладку свойств для расширяемого элемента управления.

Один элемент управления ASP.NET может расширяться несколькими расширителями элемента управления. На странице свойств для расширяемого элемента управления будут перечислены все расширители элемента управления, связанные с элементом управления.

> [!div class="step-by-step"]
> [Назад](get-started-with-the-ajax-control-toolkit-vb.md)
> [Вперед](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
