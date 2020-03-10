---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: Часть 2. уровень доступа к данным | Документация Майкрософт
author: JoeStagner
description: В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 2 описывается добавление уровня доступа к данным.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462654"
---
# <a name="part-2-data-access-layer"></a>Часть 2. уровень доступа к данным

кем [Джо Stagner)](https://github.com/JoeStagner)

> В Tailspin Spyworks. демонстрируется, как чрезвычайно прост в создании мощных масштабируемых приложений для платформы .NET. Здесь показано, как использовать замечательные новые функции в ASP.NET 4 для создания Интернет-магазина, включая покупку, оформление и администрирование.
> 
> В этой серии руководств подробно описаны все шаги, предпринятые для создания примера приложения Tailspin Spyworks. В части 2 описывается добавление уровня доступа к данным.

## <a id="_Toc260221668"></a>Добавление уровня доступа к данным

Приложение электронной коммерции будет зависеть от двух баз данных.

Для получения сведений о клиенте мы будем использовать стандартную базу данных членства ASP.NET. Для нашей покупательской корзины и каталога продуктов мы создадим базу данных SQL Express, как показано ниже.

![](tailspin-spyworks-part-2/_static/image1.jpg)

Создавайте базу данных (Commerce. mdf) в папке данных приложения\_. мы можем приступить к созданию нашего уровня доступа к данным с помощью Entity Framework .NET.

Мы создадим папку с именем "доступ к данным\_доступом", и щелкните правой кнопкой мыши эту папку и выберите команду "добавить новый элемент".

В элементе "установленные шаблоны" и выберите "ADO.NET EDM" введите EDM\_Commerce. EDMX в качестве имени и нажмите кнопку "Добавить".

![](tailspin-spyworks-part-2/_static/image2.jpg)

Выберите "создать из базы данных".

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

Сохраните и создайте.

Теперь мы готовы к добавлению нашей первой функции — меню категории продукта.

> [!div class="step-by-step"]
> [Назад](tailspin-spyworks-part-1.md)
> [Вперед](tailspin-spyworks-part-3.md)
