---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: Приступая к работе с набором средств AJAX Control Toolkit (VB) | Документация Майкрософт
author: microsoft
description: Изучите все, что нужно знать, чтобы приступить к работе с набором средств AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497142"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>Начало работы с набором элементов управления AJAX (VB)

по [Майкрософт](https://github.com/microsoft)

> Изучите все, что нужно знать, чтобы приступить к работе с набором средств AJAX Control Toolkit.

AJAX Control Toolkit содержит более 30 бесплатных элементов управления, которые можно использовать в приложениях ASP.NET. В этом руководстве вы узнаете, как загрузить набор средств AJAX Control Toolkit и добавить элементы управления набора средств в панель элементов Visual Studio или Visual Web Developer Express.

## <a name="downloading-the-ajax-control-toolkit"></a>Загрузка набора средств AJAX Control Toolkit

[AJAX Control Toolkit](http://devexpress.com/act) — это проект с открытым исходным кодом, разработанный членами сообщества ASP.NET и группой ASP.NET.

[![Загрузка набора средств AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**Рис. 01**. Загрузка набора средств AJAX Control Toolkit ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))

После загрузки файла необходимо разблокировать файл. Щелкните правой кнопкой мыши файл, выберите пункт Свойства и нажмите кнопку **разблокировать** (см. рис. 2).

[![разблокировки ZIP-файла набора средств AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**Рис. 02**. Разблокирование ZIP-файла набора средств AJAX Control Toolkit ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))

После разблокировки файла можно распаковать его: щелкните файл правой кнопкой мыши и выберите пункт **извлечь все** . Теперь мы готовы к добавлению набора средств в область элементов Visual Studio/Visual Web Developer.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Добавление набора средств AJAX Control Toolkit на панель элементов

Самый простой способ использовать AJAX Control Toolkit — добавить набор средств в панель элементов Visual Studio или Visual Web Developer (см. рис. 3). Таким образом, вы можете просто перетащить элемент управления набором средств на страницу, когда хотите его использовать.

[в панели элементов отображается ![AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**Рис. 03**. набор средств управления AJAX отображается в области элементов ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))

Сначала необходимо добавить вкладку AJAX Control Toolkit на панель элементов. Выполните следующие действия.

1. Создайте веб-сайт ASP.NET, выбрав файл параметров меню, новый веб-сайт. Дважды щелкните Default. aspx в окне обозреватель решений, чтобы открыть файл в редакторе.
2. Щелкните правой кнопкой мыши панель элементов, расположенную под вкладкой Общие, и выберите пункт меню **Добавить вкладку** (см. рис. 4).
3. Введите новую вкладку с именем набор средств управления AJAX.

[![Добавление новой вкладки](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**Рис. 04**. Добавление новой вкладки ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))

Далее необходимо добавить элементы управления AJAX Control Toolkit на новую вкладку. выполните следующие действия.

- Щелкните правой кнопкой мыши под вкладкой AJAX Control Toolkit и выберите пункт меню **элементы (см. рис. 5)** .
- Перейдите к расположению, в котором был распакован набор элементов управления AJAX, и выберите сборку Ажаксконтролтулкит. dll.

[![выбрать элементы для добавления в панель элементов](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**Рис. 05**. Выбор элементов для добавления на панель элементов ([щелкните, чтобы просмотреть изображение с полным размером](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))

После выполнения этих действий все элементы управления набора инструментов будут отображаться на панели элементов.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Обновление до новой версии набора средств

Если вы использовали более старую версию набора средств и теперь вам нужно перейти к более поздней версии, рекомендуем выполнить следующие действия.

- Двоичные файлы. Удалите старую версию сборки Ажаксконтролтулкит. dll из папки Bin веб-сайта.
- Элементы панели элементов — Удалите вкладку AJAX Control Toolkit и выполните описанные выше действия, чтобы повторно создать вкладку с новой версией сборки Ажаксконтролтулкит. dll.

> [!div class="step-by-step"]
> [Назад](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [Вперед](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
